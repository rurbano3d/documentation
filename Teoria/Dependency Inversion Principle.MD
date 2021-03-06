### S.O.L.I.D - Dependency Inversion (Inversão de dependência)
*A inversão de dependência é a estratégia de depender de interfaces ou classes abstratas, ao invés de classes concretas.*
*Módulos de alto nível não devem depender de módulos de baixo nível. Ambos devem depender de abstrações;
Abstrações não devem depender de detalhes. Detalhes devem depender de abstrações. (MARTIN 1996)*

([Saiba mais]( https://medium.com/contexto-delimitado/o-princ%C3%ADpio-da-invers%C3%A3o-de-depend%C3%AAncia-d52987634fa9#:~:text=A%20invers%C3%A3o%20de%20depend%C3%AAncia%20%C3%A9,ao%20inv%C3%A9s%20de%20classes%20concretas.))

Para criar um DIP (Dependency Inversion Principle), importo a interface e adiciono ela no constructor.Ou seja, preciso informar para o *service* qual é o *repository*

```ts
import IAppointmentsRepository from '../repositories/IAppointmentsRepository';

interface IRequest{
  provider_id: string;
  date:Date;
}

class CreateAppointmentService {
  constructor(private appointmentsRepository: IAppointmentsRepository) {}
  
  public async execute({ provider_id, date }: IRequest): Promise<Appointment> {
    //...
    const findAppointmentsInSameDate = await this.appointmentsRepository.findByDate(
      appointmentDate,
    );
    //...
  }  
 }
```

Porém precisamos intânciar o *repository* em algum lugar, como *service* esta em camada de baixo nível e o *repository* que está na camada alto nível utilizamos a DIP para evitar um acoplamento.

Então vamos instânciar o *repository* em um arquivo da mesma camada que ele. Vamos fazer isso no *appointments.routes.ts*
```ts
  //...
  import AppointmentsRepository from '../typeorm/repositories/AppointmentsRepository';

  const appointmentsRepository = new AppointmentsRepository();
  //...
  appointmentsRouter.post('/', async(request, response) => {
    const appointmentsRepository = getCustomRepository(Appointment)
  }
```
