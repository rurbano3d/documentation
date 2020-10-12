# JEST

Jest é um poderoso Framework de Testes em JavaScript com um foco na simplicidade.

Funciona com projetos usando: Babel, TypeScript, Node, React, Angular, Vue e muito mais!

## Jest no React

```
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

