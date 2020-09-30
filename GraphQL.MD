# GraphQL - Graph Query Language (Linguagem de consulta de dados em grafos).


* Foi desenvolvida pelo Facebook em 2012.
* É utilizada quando você possui vários clientes. (Flexibilidade)
* Respeita a ordem da requisição.
* Retorna mais ou menos dados de acordo com a necessidade. (Flexibilidade)
* Multíplas queries e mutations dentro da mesma requisição. 
* Modelo de dados é muito parecido com especificações de objetos a partir da orientação de objetos.
  * Atributos
  * Herança usando Interfaces
* Diferença sobre REST
  * Sem Nesting (aninhamento)
  * Sem Overfetching (obter mais dados do que o necessário).
  * Menos requisição HTTP quando a estrutura de dados é um pouco mais complexa.


Query -> obter informçãoes

Mutation -> Manipular dados

Subcription -> quando você quer ouvir uma informação em realtime.

Scalar Types -> String, Int, Boolean, Float e ID

Diferenças entre REST X GRAPHQL

- Em REST utilizamos várias rotas no backend e no GRAPHQL passamos a utilizar apenas uma rota e determinamos o recurso que queremos acessar pelo corpo da requisição. 

```js
# API Rest
GET /users
POST /users
PUT /users/:id
DELETE /users/:id
________

#GraphQL
POST /graphql
{
  query todosUsuarios{
    users()
  }
  
  query todosPedidos{
    orders( { per_page:20, page:2, filter: { nome: { "starts_with" : "Rodrigo" } } } ){
      id
      name
      groups{
        id
        title
      }
    }
  }
  
  mutation atualizaUser{
    updateUser(id:1){
      nome: "Rodrigo"
    }
  }
}

```

##### O que é Grafo?
Um grafo, possui vários pontos, chamados de nó e ligados uns aos outros. Cada nó pode ser entendido como um recurso do sistema. Um recurso pode ser um usuário, um cliente, uma pessoa e outro recurso pode ser o país do usuário, a peça fornecida pelo fornecedor, e assim por diante.

Dessa forma, o GraphQL permite a ligação entre recursos do sistema em forma de grafo.

##### O que é um ENUM?
https://medium.com/typescript/typescript-enums-1f5cc877aaa3

##### O que é Batch Operation?
https://www.youtube.com/watch?v=x6TwzA2yh08 9:00 min

##### Como Cachear os dados?
https://www.youtube.com/watch?v=x6TwzA2yh08 10:00 min


Fonte: Rocketseat, https://www.youtube.com/watch?v=oD8GqurXZ-0&t=1006s
Fonte: Código Fonte TV, https://www.youtube.com/watch?v=xbLpIhCsIdg
Fonte: https://blog.impulso.network/introducao-ao-graphql/#:~:text=GraphQL%20%C3%A9%20uma%20especifica%C3%A7%C3%A3o%20de,como%20um%20recurso%20do%20sistema.&text=Dessa%20forma%2C%20o%20GraphQL%20permite,sistema%20em%20forma%20de%20grafo.
Fonte: DevPleno ,https://www.youtube.com/watch?v=x6TwzA2yh08
Fonte: Matheus Silva, https://www.youtube.com/watch?v=7RoHxSGVAdU
