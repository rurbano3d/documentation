# Elementos de array e Async Storage

A idéia neste artigo é lidar com elementos de uma array e como salva-los em um storage.
Nos exemplos estamos utilizando javascript e o Async storage do React Native.

Antes vamos falar um pouco de como lidar com elementos em um array. Este elementos podem ser apenas uma string ou um objeto, o importante é saber lidar com qualquer tipo de informação que tem dentro do array.
Aqui vou utilizar apenas alguns métodos, caso tenha interesse em conhecer mais, [acesse aqui](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Array).

#### array.map()

```js
var soldiers = ['Resistance Trooper', 'Imperial Army'];

soldiers.map(soldier => console.log(soldier));

// Resistance Trooper
// Imperial Army
```



