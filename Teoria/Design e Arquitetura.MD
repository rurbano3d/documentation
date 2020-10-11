# Design e Arquitetura


## Arquitetura

É o processo de converter flexibilidade, escalabilidade, viabilidade, reutilização e segurança em uma solução estruturada que atenda às expectativas técnicas e de negócios.

Alguns padrões de arquitetura
* MicroServices
* Padrão em camadas
* Padrão orientado a eventos
* Padrão serverless

### Teoria DDD - Domain Driven Design ( apenas backend)

* Dividir o código por módulos (domínios)
* Separação da área de dóminio, da regra de negócios.
* Separação da camada de infra, que são as ferramentas que escolhemos para se relacionar com a área de domínio. por ex: express, mysql, adonis, etc.

Domínio: Qual a área de conhecimento daquele módulo/arquivo.

Exemplo de domínio em DDD:

```
src
└── modules
    └── appointments
    |   └── services
    |   └── repositories
    |   └── entities               
    └── users
    |   └── services
    |   └── repositories
    |   └── entities 
    └── shared
        └── database
        └── errors
        └── middlewares
        └── routes  
```
* shared - o que é compartilhado entre mais de um módulo. 
* repositories - onde fica a regra de negócio
* services -
* entities -

Infra: são as ferramentas que escolhemos para se relacionar com nossa camada de domínio.
```
src
└── modules
    └── appointments
    |   └── services
    |   └── repositories
    |   └── infra
    |       └── typeorm
    |       |   └── entities 
    |       └── http
    |           └── routes 
    └── users
    |   └── services
    |   └── repositories
    |   └── infra
    |       └── typeorm
    |       |   └── entities 
    |       └── http
    |           └── middlewares
    |           └── routes 
    └── shared
        └── infra
        |   └── typeorm(antigo database)
        |       └── http
        |           
        |           └── routes
        └── errors
     
```

* infra - as ferramentas. 
* http - tudo relacionado a camada de http. o Express por exemplo.Tudo relacionado a protocolo de comunicação.
* typeorm

### S.O.L.I.D - Liskov Substitution Principle
Integrações com banco de dados, bibliotecas ...
Entender o que é getRepository, Repository do TypeORM

Alguns arquivos ainda estão dependentes da camada de infra. Por isso é responsabilidade da camada de domínio definir quais métodos estes arquivos irão ter, por meio da *Interface*

#### Criando interface de métodos
Exemplo de um arquivo de interface
```ts
import Appointment from '../infra/typeorm/entities/Appointment';

export default interface IAppointmentsRepository {
  findByDate(date: Date): Promise<Appointment | undefined>;
}
```

Como chama-lo 
```ts
import IAppointmentsRepository from '@modules/appointments/repositories/IAppointmentsRepository';

class AppointmentsRepository extends Repository<Appointment>
  implements IAppointmentsRepository {}
```

#### Conceito DTOs (Data Transfers Objects)
sempre que precisar tipar uma informação composta, utilizada para criar, editar, listar.

### S.O.L.I.D - Dependency Inversion (Inversão de dependência)
*A inversão de dependência é a estratégia de depender de interfaces ou classes abstratas, ao invés de classes concretas.*
*Módulos de alto nível não devem depender de módulos de baixo nível. Ambos devem depender de abstrações;
Abstrações não devem depender de detalhes. Detalhes devem depender de abstrações. (MARTIN 1996)*

https://medium.com/contexto-delimitado/o-princ%C3%ADpio-da-invers%C3%A3o-de-depend%C3%AAncia-d52987634fa9#:~:text=A%20invers%C3%A3o%20de%20depend%C3%AAncia%20%C3%A9,ao%20inv%C3%A9s%20de%20classes%20concretas.

Para criar um DIP (Dependency Inversion Principle), importo a interface e adiciono ela no constructor.

```ts
import IAppointmentsRepository from '../repositories/IAppointmentsRepository';

class CreateAppointmentService {
  constructor(private appointmentsRepository: IAppointmentsRepository) {}
  
  public async execute({ provider_id, date }: IRequest): Promise<Appointment> {
    const findAppointmentsInSameDate = await this.appointmentsRepository.findByDate(
      appointmentDate,
    );
  }  
 }
```
## Injeção de dependência
Library em React - tsyringe
https://github.com/microsoft/tsyringe


## Design
Responsável pelo design do nível de código.

Alguns padrões de design
* Factory Pattern
* Adapter Pattern
 


fonte: GOStack -  Rocketseat
fonte: https://medium.com/@oieduardorabelo/arquitetura-de-software-a-diferen%C3%A7a-entre-arquitetura-e-design-964ab38ea61a
fonte: Modular Programming with Javascript, Sasan Seydnejad
fonte: https://medium.com/contexto-delimitado/o-princ%C3%ADpio-da-invers%C3%A3o-de-depend%C3%AAncia-d52987634fa9#:~:text=A%20invers%C3%A3o%20de%20depend%C3%AAncia%20%C3%A9,ao%20inv%C3%A9s%20de%20classes%20concretas.
