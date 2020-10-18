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
const CreateAppointmentService = new CreateAppointmentService(appointmentsRepository);
```

É substituído por 
```ts
import CreateAppointmentService from '@modules/appointments/services/CreateAppointmentService';

const CreateAppointmentService = new CreateAppointmentService();
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
