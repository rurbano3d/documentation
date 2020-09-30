# Primeiro código com GraphQL

Iniciar o projeto node.

```
yarn init -y
```

Instalar o Apollo Server e o GraphQL

```
yarn add apollo-server graphql
```

Vamos iniciar o apollo e iniciar nosso GraphQL
```js
const { ApolloServer, gql } = require("apollo-server");

const typeDefs = gql`
  type Query {
    hello: String
  }
`;
const resolvers = {
  Query: {
    hello: () => "Hello world",
  },
};

const server = new ApolloServer({ typeDefs, resolvers });
server.listen().then(({ url }) => console.log(` 🚀 Server started at ${url}`));
```

TypeDefs -> é o schema do graphQL. Onde modelamos os dados, fazemos as queries e mutations

Resolvers ->  é as açoes que as queries e as mutations vão tomar.

O que é o Apollo Server?
https://www.apollographql.com/docs/apollo-server/

Emoji no Mac e Vscode -> Ctrl+Cmd+Space

Extensão vscode - *GraphQL* extension for vscode.


Fonte: Mateus Silva, https://www.youtube.com/watch?v=iUYabIGhJYk
Fonte: Emerson Pereira, https://medium.com/@emerson_pereira/montando-api-graphql-em-node-js-com-apollo-e-mongodb-6b5089ff10d3
