# Injeção de dependência

Em NodeJs com Typescritp utilizaremos uma library chamada *tsyring*. [Saiba Mais](https://github.com/microsoft/tsyringe)

```shell
  yarn add tsyringe
```

Agora precisamos criar um arquivo que fica controlando as injeções de dependência. É ele que diz para o nosso *service* qual *repository* será injetado.

> service - objeto que contém lógica de negócio que não pertence naturalmente a nenhuma entidade.
> repository - objeto que contém lógica de negócio que pertence a uma entidade.

@shared/container/index.ts
```ts
import { container } from 'tsyringe';

import InterfaceDoRepositorio from '@modules/...';
import Repositorio from '@modules/...';

container.registerSingleton<InterfaceDoRepositorio>('Name', Repositório);
```
Exemplo prático.
```ts
import { container } from 'tsyringe';

import IAppointmentsRepository from '@modules/appointments/repositories/IAppointmentsRepository';
import AppointmentsRepository from '@modules/appointments/infra/typeorm/repositories/AppointmentsRepository';

container.registerSingleton<IAppointmentsRepository>('AppointmentsRepository', AppointmentsRepository);
```
Diferença entre *registerSingleton* e *register*.
> registerSingleton - ele instância a classe apenas uma única vez durante toda ciclo de vida da aplicação 
> register - toda vez que um arquivo diferente precisar do *repository* ele instância uma nova classe, gerando várias instâncias de uma mesma classe.

[Singleton Pattern](https://www.dofactory.com/javascript/design-patterns/singleton)

Precisamos importar o arquivo acima em algume lugar, neste caso importei ele no arquivo *server.js*

```ts
  import '@shared/container;'
```

Uma observação. A injeção de dependência substitui a forma de ficar adicionando manualmente um repositório e também o acoplamento.
Por exemplo
```ts
import AppointmentsRepository from '@modules/appointments/infra/typeorm/repositories/AppointmentsRepository';
import CreateAppointmentService from '@modules/appointments/services/CreateAppointmentService';

const appointmentsRepository = new AppointmentsRepository();
const createAppointmentService = new CreateAppointmentService(appointmentsRepository);
```

É substituído por 
```ts
import {container} from 'tsyring';

import CreateAppointmentService from '@modules/appointments/services/CreateAppointmentService';

const createAppointmentService = container.resolve(CreateAppointmentService);
```

porque dentro de *CreateAppointmentService* eu injetei o repositório *AppointmentsRepository*.

```ts
import {injectable, inject} from 'tsyringe';

import IAppointmentsRepository from '../repositories/IAppointmentsRepository';

@injectable()
class CreateAppointmentService {
  constructor(
    @injectable('AppointmentsRepository') private appointmentsRepository: IAppointmentsRepository,
  ){}
}
```
