# DDD - Domain Driven Design

## Camadas

### Domain
#### Entities
Ficam as Entities, o core da nossa aplicação.

User, Address, etc

### Application
#### Repository
#### Use Cases / Services

### Framework
#### GRPC
Recebe as chamadas

#### DB
Conexão com o Banco de dados

## Fluxo de dados

Fazemos uma chamada para aplicação --> Framework recebe a chamada --> chama o Use Cases/Services --> chama o Repository -> que via injeção de dependência chama o DB (Framework)--> chama o Domain
