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

## Design
Responsável pelo design do nível de código.

Alguns padrões de design
* Factory Pattern
* Adapter Pattern
 
### S.O.L.I.D (design de software)

fonte: GOStack -  Rocketseat
fonte: https://medium.com/@oieduardorabelo/arquitetura-de-software-a-diferen%C3%A7a-entre-arquitetura-e-design-964ab38ea61a
font: Modular Programming with Javascript, Sasan Seydnejad
