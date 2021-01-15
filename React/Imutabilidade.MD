## O que é imutabilidade?

Imutabilidade é algo que não pode mudar, ou seja em programação é um objeto que não sofre alterações no seu estado.

## O que é objeto?

Em programação é uma referência a um local da memória que possui um valor. Podendo ser uma variável, função ou estrutura de dados.

## O que é estado?

Estado em programação é um termo técnico para todas as informações armazendas ou o valor do objeto.

*Uma referência na memoria local é imutável quando suas informações(valor) não são alteradas.*

## Então como funciona a alteração do valor em um objeto imutável?

Como o objeto é imutável ele não altera seu valor mas sim é criado um novo objeto com o valor novo.
Como mostrado perfeitamente por [Corey Schafer](https://www.youtube.com/watch?v=5qQQ3yzbKp8).

## Vantagem no React

Ao criar um novo objeto e manter o objeto antigo nos conseguimos identificar rapidamente se o objeto foi alterado, sabendo assim que precisamos renderiza-lo novamente.

"Se a referência para o objeto atual é diferente da anterior, então o objeto mudou" - Antonio Milesi Bastos

## Como funciona no código

Em React para "alterarmos" um objeto imutável criamos um novo objeto e copiamos a informação do objeto antigo e adicionamos a informação que será alterada.
```js
const prequelStarWars = {name:'Anakin Skywalker', category:'Jedi'};

const classicStarWars = { ...prequelStarWars, category: 'Sith'};
```

Quando lidamos com objetos profundamente aninhados, atualiza-los de uma forma imutável pode parecer complexo. Bibliotecas com o [Immer](https://github.com/immerjs/immer) pode ajudar.

## Immer
[Doc](https://immerjs.github.io/immer/docs/produce)


## Saiba mais:
[Mutável X Imutável - Corey Schafer](https://www.youtube.com/watch?v=5qQQ3yzbKp8)

[Por que imutabilidade é importante - Antonio Milesi Bastos](https://desenvolvedor.expert/por-que-imutabilidade-eh-importante-fd0ba22f103e)

[O poder da imutabilidade - React](https://reactjs.org/docs/optimizing-performance.html#the-power-of-not-mutating-data)









