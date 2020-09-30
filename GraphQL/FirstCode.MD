# Primeiro código com GraphQL

Iniciar o projeto node.

```
yarn init -y
```

Instalar o Apollo Server e o GraphQL

```
yarn add apollo-server graphql
```

Instalar o Nodemon como desenvolvimento para live reload do server!

```
yarn add nodemon -D
```
E acrescenta em *package.json*
```json
"scripts": {
    "dev": "npx nodemon src/index.js"
  },
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

No Playground do GraphQL
```gql
{
 hello
}
___________

{
  "data": {
    "hello": "Hello world"
  }
}
```

Vamos adicionar algumas Entidades simples e aninhadas (nesting)
```js
const { ApolloServer, gql } = require("apollo-server");

const typeDefs = gql`
  type User {
    _id: ID!
    name: String!
    email: String!
    active: Boolean!
  }

  type Post {
    _id: ID!
    title: String!
    content: String!
    author: User!
  }

  type Query {
    hello: String
    users: [User!]!
    # users: [User]! pode retornar um array vazia[], mas não retorna NULL.
    # users: [User!]! pode retornar um array vazia[] ou [{}], mas não retorna [NULL].
  }
`;
const resolvers = {
  Query: {
    hello: () => "Hello world",
    users: () => [
      {
        _id: String(Math.random()),
        name: "Rodrigo",
        email: "rodrigo@gmail.com",
        active: true,
      },
      {
        _id: String(Math.random()),
        name: "Rodrigo 2",
        email: "rodrigo2@gmail.com",
        active: false,
      },
      {
        _id: String(Math.random()),
        name: "Rodrigo 3",
        email: "rodrigo3@gmail.com",
        active: true,
      },
    ],
  },
};

const server = new ApolloServer({ typeDefs, resolvers });
server.listen().then(({ url }) => console.log(` 🚀 Server started at ${url}`));
```
! -> você esta dizendo que o atributo é obrigatório, caso a informção volte como NULL o playground informa que há um erro.

No Playground do GraphQL
```gql
{
   users{
    name
    email
    active
  }
}
___________

{
  "data": {
    "users": [
      {
        "name": "Rodrigo",
        "email": "rodrigo@gmail.com",
        "active": true
      },
      {
        "name": "Rodrigo 2",
        "email": "rodrigo2@gmail.com",
        "active": false
      },
      {
        "name": "Rodrigo 3",
        "email": "rodrigo3@gmail.com",
        "active": true
      }
    ]
  }
}
```

Vamos utilizar um find neste exemplo
```js
const { ApolloServer, gql } = require("apollo-server");

const users = [
  {
    _id: String(Math.random()),
    name: "Rodrigo",
    email: "rodrigo@gmail.com",
    active: true,
  },
  {
    _id: String(Math.random()),
    name: "Rodrigo 2",
    email: "rodrigo2@gmail.com",
    active: false,
  },
  {
    _id: String(Math.random()),
    name: "Rodrigo 3",
    email: "rodrigo3@gmail.com",
    active: true,
  },
];

const typeDefs = gql`
  type User {
    _id: ID!
    name: String!
    email: String!
    active: Boolean!
  }

  type Query {
    hello: String
    users: [User!]!
    getUserByEmail(email: String!): User!
  }
`;
const resolvers = {
  Query: {
    users: () => users,
    getUserByEmail: (_, args) => {
      return users.find((user) => user.email === args.email);
    },
  },
};

const server = new ApolloServer({ typeDefs, resolvers });
server.listen().then(({ url }) => console.log(` 🚀 Server started at ${url}`));

```

No Playground do GraphQL
```gql
query{
  getUserByEmail(email: "rodrigo@gmail.com"){
    name
    email
  }
}
___________

{
  "data": {
    "getUserByEmail": {
      "name": "Rodrigo",
      "email": "rodrigo@gmail.com"
    }
  }
}
```

Por último vamos utilizar um *mutation*
```js
const { ApolloServer, gql } = require("apollo-server");

const users = [
  {
    _id: String(Math.random()),
    name: "Rodrigo",
    email: "rodrigo@gmail.com",
    active: true,
  },
  {
    _id: String(Math.random()),
    name: "Rodrigo 2",
    email: "rodrigo2@gmail.com",
    active: false,
  },
  {
    _id: String(Math.random()),
    name: "Rodrigo 3",
    email: "rodrigo3@gmail.com",
    active: true,
  },
];

const typeDefs = gql`
  type User {
    _id: ID!
    name: String!
    email: String!
    active: Boolean!
  }

  type Query {
    users: [User!]!
  }

  type Mutation {
    createUser(name: String!, email: String!): User!
  }
`;
const resolvers = {
  Query: {
    users: () => users,
  },
  Mutation: {
    createUser: (_, args) => {
      const newUser = {
        _id: String(Math.random()),
        name: args.name,
        email: args.email,
        active: true,
      };
      users.push(newUser);
      return newUser;
    },
  },
};

const server = new ApolloServer({ typeDefs, resolvers });
server.listen().then(({ url }) => console.log(` 🚀 Server started at ${url}`));

```

No Playground do GraphQL
```gql
mutation{
  createUser(name:"Mariana", email:"mariana@gmail.com"){
    _id
    name
  }
}
___________

{
  "data": {
    "createUser": {
      "_id": "0.8070866112378954",
      "name": "Mariana"
    }
  }
}
```


O que é o Apollo Server?
https://www.apollographql.com/docs/apollo-server/

Emoji no Mac e Vscode -> Ctrl+Cmd+Space

Extensão vscode - *GraphQL* extension for vscode.


Fonte: Mateus Silva, https://www.youtube.com/watch?v=iUYabIGhJYk
Fonte: Emerson Pereira, https://medium.com/@emerson_pereira/montando-api-graphql-em-node-js-com-apollo-e-mongodb-6b5089ff10d3
