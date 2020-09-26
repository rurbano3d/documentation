# Typescript

## Organizando o caminho de imports

Em *tsconfig.json
```json
  "baseUrl":"de onde parte o caminho",
  "paths":{
    "@nome do atalho do caminho/*":["pasta do projeto/*"],
  }
```
* */** este simbolo significa tudo que vem depois da barra

Exemplo
```json
  "baseUrl":"./src",
  "paths":{
    "@modules/*":["modules/*"],
    "@config/*":["config/*"],
    "@shared/*":["shared/*"],
  }
```

É necessário adicionar uma Lib para o *ts-node* entender os novos atalhos.
```
yarn add tsconfig-paths -d
```
E dentro do package.json adicionamos *tsconfig-paths/register*.

```json
"scripts:{
  "dev:server": "ts-node-dev -r tsconfig-paths/register --inspect --transpileOnly --ignore-watch node_modules src/shared/infra/http/server.ts",
  "typeorm": "ts-node-dev tsconfig-paths/register ./node_modules/typeorm/cli.js"
}
```
