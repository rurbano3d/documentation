# JEST

Jest é um poderoso Framework de Testes em JavaScript com um foco na simplicidade.

Funciona com projetos usando: Babel, TypeScript, Node, React, Angular, Vue e muito mais!

## Jest no React

```shell
yarn add jest -D

yarn jest --init
``` 
- Would like to use Jest when running "test" script in "package.json"? - Yes
- Choose the test enviroment that will be used for testing - Node
- Do you want Jest to add coverage reports? - no
- Automatically clear mock calls and instances between every test? - Yes

É gerado um arquivo *jest.config.js*

Para utilizar o Jest com Typescript
```
  yarn add ts-jest -D
  yarn add @types/jest -D
```

Em *jest.config.js* habilite.
```js
preset: 'ts-jest',

testMatch: [
   "**/*.spec.ts"
  ],
```
Se você utiliza *eslint*
```json
"env":{
  "jest":true
}
```

Exemplo simples
```ts
test('sum two numbers', () =>{
  expect(1+2).toBe(3);
});
```

Se você estiver utilizando o *tsconfig-paths* para resolver os caminhos, em *jest.config.js*, é preciso adicionar;
```js
  const{ pathsToModuleNameMapper } = require('ts-jest/utils');
  const{ compilerOptions } = require('./tsconfig.json');
  
  module.exports={
  ...
  
  moduleNameMapper: pathsToModuleNameMapper(compilerOptions.paths, { prefix: '<rootDir>/src/'}),
  
```
Obs: O Javascript não suporta comentário no JSON, portanto é necessário tirar todos os comentários do arquivos *tsconfig.json*


## Coverage

Ferramenta que já vem no Jest, que serve para saber o que falta para testar, o que você já testou, etc.

Dentro de *jest.config.js*
```js
collectCoverage: true,

collectCoverageFrom:[
  '<rootDir>/src/modules/**/services/*.ts'
],
  
coverageDirectory: 'coverage',

coverageReporters:[
  "text-summary",
  "lcov",
],
```

### Funções do JEST

> spyOn - permite você mockar todo um módulo ou uma função individual do módulo. No seu conceito geral é usado para rastrear chamadas de métodos.
```ts
const sendMail = jest.spyOn(fakeMailProvider, 'sendMail');
```

> beforeEach, afterEach - permite executar um código antes ou depois de cada teste, ou melhor, cada *it*

Neste exemplo intâncias de reposítorios que são criadas em cada *it*, eu consigo reduzir e não repetir o código utilizando a função *beforeEach*
```ts
//...
let fakeUsersRepository: FakeUsersRepository;
let fakeMailProvider: FakeMailProvider;
let sendForgotPasswordEmailService: SendForgotPasswordEmailService;

describe('ForgotPassword', () => {
  beforeEach(() => {
    fakeUsersRepository = new FakeUsersRepository();
    fakeMailProvider = new FakeMailProvider();
    
    sendForgotPasswordEmailService = new SendForgotPasswordEmailService(
      fakeUsersRepository,
      fakeMailProvider,
      
    );
  });

  it('should be able to recover the password using the email', async () => {
    //...
```
