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
Para isso precisamos instanciar o *service* de Forgot Password e executa-lo, através do método *exxecute*.

```ts
import FakeUsersRepository from '../repositories/fakes/FakeUsersRepository';

describe('ForgotPassword', () => {
  it('should be able to recover the password using the email', async () => {
  const fakeUsersRepository = new FakeUsersRepository();
  
  const sendForgotPasswordEmailService = new SendForgotPasswordEmailService();
  
  await fakeUsersRepository.create({
      name: 'John Doe',
      email: 'johndoe@example.com',
      password: '123456',
    });
  
  await sendForgotPasswordEmailService.execute({
      email: 'johndoe@example.com',
    });
    
  });
```


