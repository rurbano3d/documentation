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

Utilizar o typeScript em objects.keys

```js
type SimpleObject = {
  visa: RegExp;
  mastercard: RegExp;
  amex: RegExp;
  discover: RegExp;
  diners_club: RegExp;
  jcb: RegExp;
};

const checkCreditCardIsSupported = (number: string) => {
  const acceptedCreditCards: SimpleObject = {
    visa: /^4[0-9]{12}(?:[0-9]{3})?$/,
    mastercard: /^5[1-5][0-9]{14}$|^2(?:2(?:2[1-9]|[3-9][0-9])|[3-6][0-9][0-9]|7(?:[01][0-9]|20))[0-9]{12}$/,
    amex: /^3[47][0-9]{13}$/,
    discover: /^65[4-9][0-9]{13}|64[4-9][0-9]{13}|6011[0-9]{12}|(622(?:12[6-9]|1[3-9][0-9]|[2-8][0-9][0-9]|9[01][0-9]|92[0-5])[0-9]{10})$/,
    diners_club: /^3(?:0[0-5]|[68][0-9])[0-9]{11}$/,
    jcb: /^(?:2131|1800|35[0-9]{3})[0-9]{11}$/,
  };

  const value = number.replace(/\D/g, '');
  let accepted = false;
  let length1 = 19;

  Object.keys(acceptedCreditCards).forEach((key) => {
    const regex = acceptedCreditCards[key as keyof SimpleObject];
    if (regex.test(value)) {
      accepted = true;
      length1 = 16;
    }
  });

  return { accepted, length1 };
};

```

