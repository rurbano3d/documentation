
#S.O.L.I.D - Liskov Substitution Principle

[Saiba Mais](https://medium.com/contexto-delimitado/o-princ%C3%ADpio-da-substitui%C3%A7%C3%A3o-de-liskov-df5648906fbe0)

> Camadas que são integração com banco de dados ou outras ferramentas devem ser possível substituir estas informações definindo um conjunto de regras pra ela. Nosso *service* não deve conhecer a formato final da estrutura que armazena nosso dados, a persistência de nossos dados.


Aqui temos um *repository*, dentro da nossa camada de domínio, que esta totalmente dependente de um módulo de baixo nível, no caso a camada de typeorm.
```ts
import { EntityRepository, Repository } from 'typeorm';

import Appointment from '../infra/typeorm/entitites/Appointment';

@EntityRepository(Appointment)
class AppointmentRepository extends Repository<Appointment>{
  public async findByDate(date:Date):Promise<Appointment | undefined>{
    const findAppointment = await this.findOne({
      where: { date },
    });
    
    return findAppointment | undefined;
  }
}

export defautl AppointmentRepository;
```

Para resolver esta situação movemos este arquivo para a camada de typeorm, deixando este *repository* no mesmo nível que o typeorm.

>@modules/appointments/repositories -> @modules/apoointments/infra/typeorm/repositories

Porém ainda é responsabilidade da nossa camada de domínio definir quais métodos este *repository* possui. Pois caso há necessidade de trocar o banco de dados ou o ORM desta aplicação manteremos o funcionamento dela.
Para isso é necessário criar uma *interface* em @modules/appointments/repositories

```ts
import Appointment from '../infra/typeorm/entities/Appointment';

interface IAppointmentsRepository{
 findByDate(date:date):Promise<Appointment | undefined>;
}
```

Agora é preciso alterar um pouco nosso *repository* na camada do typeorm. para que seja implementado a interface que criamos.
```ts
import { EntityRepository, Repository } from 'typeorm';

import IAppointmentsRepository from '@modules/appointment/repositories/IAppointmentsRepository';
import Appointment from '../entitites/Appointment';

@EntityRepository(Appointment)
class AppointmentRepository extends Repository<Appointment> implements IAppointmentsRepository{
  public async findByDate(date:Date):Promise<Appointment | undefined>{
    const findAppointment = await this.findOne({
      where: { date },
    });
    
    return findAppointment;
  }
}

export defautl AppointmentRepository;
```

Note que a *class AppointmentRepository* extende *Repository<Appointment>* automaticamente nossa classe recebe métodos padrãos do typeORM como  *create*, *save*, *findOne*, etc. Porém com isso perdemos o controle do que exatamente os métodos estão fazendo, para ter controle sobre esta situação podemos incorporar as seguintes mudanças no código.

```ts
import { getRepository, Repository } from 'typeorm';

import IAppointmentsRepository from '@modules/appointment/repositories/IAppointmentsRepository';
import Appointment from '../entitites/Appointment';
import ICreateAppointmentDTO from '@modules/appointment/dtos/ICreateAppointmentDTO';

class AppointmentRepository implements IAppointmentsRepository{
  private ormRepository = getRepository(Appointment);

  constructor(){
    this.ormRepository = getRepository(Appointment);
  }
  
  public async findByDate(date:Date):Promise<Appointment | undefined>{
    const findAppointment = await this.ormRepository.findOne({
      where: { date },
    });
    
    return findAppointment;
  }
  
  public async create({ provider_id, date }:ICreateAppointmentDTO): Promise<Appointments>{
    const appointment = this.ormRepository.create({ provider_id, date });
    
    await this.ormRepository.save(appointment);
    
    return appointment;
  }
}

export defautl AppointmentRepository;
```

```ts
import Appointment from '../infra/typeorm/entities/Appointment';
import ICreateAppointmentDTO from '../dtos/ICreateAppointmentDTO';

interface IAppointmentsRepository{
 create(date:ICreateAppointmentDTO):Promise<Appointment>;
 findByDate(date:date):Promise<Appointment | undefined>;
}
```

> DTOS (data transfer objects) - Sempre que precisar tipar um informação composta, utilizada para criar, listar e editar.
