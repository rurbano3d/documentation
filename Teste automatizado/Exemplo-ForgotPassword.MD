# Forgot Password

//red
//green
//refactory


Primeiro vamos criar um *service*.

> services são objetos que contém lógica de negócio que não pertence naturalmente a nenhuma entidade.

Este *service* terá um código simples e a partir dos testes vamos incrementando o código.

```ts
export default class SendForgotPasswordEmailService {

  public async execute(): Promise<void> {
    
  }
}

```

Criação do teste unitário

```ts
describe('ForgotPassword', () => {
  it('should be able to recover the password using the email', async () => {
    
  });
});

```

Vamos passo a passo para entender todo funcionamento do teste. 
Analisando o teste nós precisamos ser capaz de recuperar a senha usando um e-mail, por ser um teste unitário precisamos criar um *user*.
Não vou entrar no repositório fake para usuário neste artigo. Abordaremos isso em outro artigo.

Para criar um *user* precisamos instanciar o reposítorio, utilizamos um repositório fake para criar um usuário fake.

O porque de usário fake e não um usuário normal? 
Ao criarmos um usuário normal ele é salvo no banco de dados. O usuário fake passa por todo o processo de criação de usuário normal mas utilizamos uma memória volátil para armazenar esta informação, não poluindo o banco de dados.

> repositories são objetos que contém lógica de negócio que pertence a um Entidade.

```ts
import FakeUsersRepository from '../repositories/fakes/FakeUsersRepository';

describe('ForgotPassword', () => {
  it('should be able to recover the password using the email', async () => {
  const fakeUsersRepository = new FakeUsersRepository();
  
  await fakeUsersRepository.create({
      name: 'John Doe',
      email: 'johndoe@example.com',
      password: '123456',
    });
    
  });
```

Depois de adicionar o usuário, precisamos enviar o email do *user* para o *service*. 
Para isso precisamos instanciar o *service* de Forgot Password e executa-lo, através do método *execute*.

```ts
import FakeUsersRepository from '../repositories/fakes/FakeUsersRepository';
import SendForgotPasswordEmailService from './SendForgotPasswordEmailService';

describe('ForgotPassword', () => {
  it('should be able to recover the password using the email', async () => {
  const fakeUsersRepository = new FakeUsersRepository();
  
  const sendForgotPasswordEmailService = new SendForgotPasswordEmailService();
  
  const user = await fakeUsersRepository.create({
      name: 'John Doe',
      email: 'johndoe@example.com',
      password: '123456',
    });
  
  const response = await sendForgotPasswordEmailService.execute({
      email: 'johndoe@example.com',
    });
    
  expect(response).toEqual(user.email);  
  });
```

Implementamos o email no *service* e com isso verificamos se esta sendo acionado o *service*.

```ts
interface IResquest{
  email: string;
}
export default class SendForgotPasswordEmailService {

  public async execute({email}:IRequest): Promise<string> {
    return email;
  }
}

```
Executamos o test somente na url que queremos e o teste passará, porém não isso que queremos. Queremos enviar um email para o usuário com as informações para ele trocar a senha.
```terminal
  yarn test src/modules/users/services/SendForgotPasswordEmailService.spec.ts
```

Vamos utilizar um provedor de email fake para enviar o e-mail, também não abordaremos este código neste artigo.

Implementamos o *FakeMailProvider* e vamos utilizar um método do *Jest* chamado *spyOn*.

> spyOn - permite você mockar todo um módulo ou uma função individual do módulo. No seu conceito geral é usado para rastrear chamadas de métodos.

No exemplo abaixo vamos utilizar o *spyOn* para rastrear o método *sendMail* do *FakeMailProvider*. E em *expect*, esperamos que o método seja chamado.

```ts
import FakeUsersRepository from '../repositories/fakes/FakeUsersRepository';
import SendForgotPasswordEmailService from './SendForgotPasswordEmailService';
import FakeMailProvider from '@shared/container/providers/MailProvider/fakes/FakeMailProvider';

describe('ForgotPassword', () => {
  it('should be able to recover the password using the email', async () => {
  const fakeUsersRepository = new FakeUsersRepository();
  const fakeMailProvider = new FakeMailProvider();
  
  const sendMail = jest.spyOn(fakeMailProvider, 'sendMail');
  
  const sendForgotPasswordEmailService = new SendForgotPasswordEmailService();
  
  await fakeUsersRepository.create({
      name: 'John Doe',
      email: 'johndoe@example.com',
      password: '123456',
    });
  
  await sendForgotPasswordEmailService.execute({
      email: 'johndoe@example.com',
    });
    
  expect(sendMail).toHaveBeenCalled();
  });
```
No *service* adicionamos o *MailProvider* como uma injeção de dependência. [Veja mais sobre injeção de dependência](https://github.com/rurbano3d/documentation/blob/master/Teoria/Inje%C3%A7%C3%A3o%20de%20depend%C3%AAncia.MD)

```ts
import { injectable, inject } from 'tsyringe';

import IMailProvider from '@shared/container/providers/MailProvider/models/IMailProvider';

interface IResquest{
  email: string;
}

@injectable()
export default class SendForgotPasswordEmailService {

  constructor(
     @inject('MailProvider') private mailProvider: IMailProvider,
  ){}

  public async execute({email}:IRequest): Promise<string> {
  
    this.mailProvider.sendMail(
      email,
      'Pedido de recuperação de senha recebido',
    );
    
  }
}

```
Se executarmos o test veremos que irá passar. Sendo assim nosso serviço já esta enviando e-mail para o usuário. Porém temos mais alguns testes a serem feitos.
É importante validar o e-mail, ou seja, verificar se o email existe, para isso vamos executar um novo teste dento do escopo *ForgotPassword*.

```ts
import FakeUsersRepository from '../repositories/fakes/FakeUsersRepository';
import SendForgotPasswordEmailService from './SendForgotPasswordEmailService';
import FakeMailProvider from '@shared/container/providers/MailProvider/fakes/FakeMailProvider';

describe('ForgotPassword', () => {
  // ...
  it('should not be able to recover a non-existing user password', async () => {
    const fakeUsersRepository = new FakeUsersRepository();
    const fakeMailProvider = new FakeMailProvider();

    const sendForgotPasswordEmailService = new SendForgotPasswordEmailService(
      fakeUsersRepository,
      fakeMailProvider,
    );

    await expect(
      sendForgotPasswordEmailService.execute({
        email: 'johndoe@example.com',
      }),
    ).rejects.toBeInstanceOf(AppError);
  });
 }
```
