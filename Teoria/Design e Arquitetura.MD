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
    |           └── entities 
    └── users
    |   └── services
    |   └── repositories
    |   
    |   └── infra
    |       └── typeorm
    |           └── entities 
    └── shared
        └── infra
        |   └── typeorm(antigo database)
        |       └── http
        |           └── middlewares
        |           └── routes
        └── errors
     
```

* infra - as ferramentas. 
* http - tudo relacionado a camada de http. o Express por exemplo.Tudo relacionado a protocolo de comunicação.
* typeorm


## Design
Responsável pelo design do nível de código.

Alguns padrões de design
* Factory Pattern
* Adapter Pattern
 
### S.O.L.I.D (design de software)

fonte: GOStack -  Rocketseat
fonte: https://medium.com/@oieduardorabelo/arquitetura-de-software-a-diferen%C3%A7a-entre-arquitetura-e-design-964ab38ea61a
font: Modular Programming with Javascript, Sasan Seydnejad
