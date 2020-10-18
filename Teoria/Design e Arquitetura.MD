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
    └── users
    └── shared 
```
* appointments - tudo que é do domínio de appointments
* users - tudo que é do domínio de users
* shared - o que é compartilhado entre mais de um módulo. 


Infra: são as ferramentas que escolhemos para se relacionar com nossa camada de domínio.
```
src
└── modules
    └── appointments
    |   └── dtos
    |   └── services
    |   └── repositories
    |   └── infra
    |       └── typeorm
    |       |   └── entities 
    |       |   └── repositories     
    |       └── http
    |           └── routes 
    |           └── controllers 
    └── users
    |   └── dtos
    |   └── services
    |   └── repositories
    |   └── infra
    |       └── typeorm
    |       |   └── entities 
    |       |   └── repositories  
    |       └── http
    |           └── middlewares
    |           └── routes 
    |           └── controllers     
    └── shared
        └── container
        └── infra
        |   └── http
        |       └── routes
        |   └── typeorm
        |       └── migrations
        └── errors
     
```
* dtos - (data transfers objects) Sempre que precisar *tipar* um informação composta, utilizada para criar, listar e editar.
```ts
export default interface ICreateUserDTO {
  name: string;
  email: string;
  password: string;
}
```
* services - Serviços são objetos que contém lógica de negócio que não pertence naturalmente a nenhuma Entidade. ([Saiba mais]( https://pt.stackoverflow.com/questions/49607/o-que-%C3%A9-a-camada-de-servi%C3%A7os-em-ddd))
* repositories - Repositórios são objetos que contém lógica de negócio que pertence a Entidade.
    * repositories dentro de typeORM contém a regra de négocio especifica do typeORM
    * repositories dentro do módulo contém a interface, ou seja, a forma abstrata que fica entre o repositório do typeORM e a camada de serviço (inversão de depedência.
    ([Saiba mais](  https://pt.stackoverflow.com/questions/12927/qual-a-diferen%C3%A7a-entre-dao-e-repository))
   
* infra - Infra é onde fica as ferramentas. 
* typeorm - onde fica as entidades e repositorio que lidam diretamente, codigo acoplados com o bando de dados.
* entities - onde fica os models 
* http - tudo relacionado a camada de http. o Express por exemplo.Tudo relacionado a protocolo de comunicação.
* routes - as rotas
* controllers - abstração dos metodos da rest (index,show,update,delete,create)
* middlewares 
* migrations 

### S.O.L.I.D - Liskov Substitution Principle
[Saiba Mais](https://github.com/rurbano3d/documentation/blob/master/Teoria/Liskov%20Substitution%20Principle.MD)

### S.O.L.I.D - Dependency Inversion (Inversão de dependência)
[Saiba Mais](https://github.com/rurbano3d/documentation/edit/master/Teoria/Dependency%20Inversion%20Principle.MD)

### Injeção de dependência
[Saiba Mais](https://github.com/rurbano3d/documentation/blob/master/Teoria/Inje%C3%A7%C3%A3o%20de%20depend%C3%AAncia.MD)


## Design
Responsável pelo design do nível de código.

Alguns padrões de design
* Factory Pattern
* Adapter Pattern
 


fonte: GOStack -  Rocketseat
fonte: https://medium.com/@oieduardorabelo/arquitetura-de-software-a-diferen%C3%A7a-entre-arquitetura-e-design-964ab38ea61a
fonte: Modular Programming with Javascript, Sasan Seydnejad
fonte: https://medium.com/contexto-delimitado/o-princ%C3%ADpio-da-invers%C3%A3o-de-depend%C3%AAncia-d52987634fa9#:~:text=A%20invers%C3%A3o%20de%20depend%C3%AAncia%20%C3%A9,ao%20inv%C3%A9s%20de%20classes%20concretas.
