## Qual problema o Context API resolve?
Sempre que precisamos compartilhar dados, estados, atributos ou propriedades, vou tratar tudo como propriedade a partir daqui,  com outros componentes encontramos situações fáceis de lidar e situações mais complexas.

Quando passamos propriedades de um componente pai para um filho e paramos por ai a utilização do props é o suficiente, pois é uma ligação direta.

Mas quando precisamos passar propriedades para vários componentes, a utilização de props se torna insustentável. 

Para resolver esta situação utilizei o conceito de Estado Global, onde armazeno a propriedade e consigo acessar ela em qualquer lugar da minha aplicação, ou melhor, em grande parte da minha aplicação.

Neste artigo vou falar sobre como o estado global tornou o acesso de propriedades bem aceitável, utilizando o CONTEXT API que é nativo do React a partir da versão 16.x.

## Introdução sobre o Context API

## Desenvolvimento com exemplos
Quero por meio deste artigo passar todo o processo que fiz para chegar ao resultado de escolher o conceito de estado global com o CONTEXT API.

No primeiro caso eu precisava apenas passar uma propriedade para um componente filho.
```js
  <DarthVader spoiler='Luke, eu sou seu pai!' />
```
```js
const DarthVader = ({spoiler}) =>{
   <Luke>
   {spoiler}
   </Luke>
}
```

No segundo caso eu precisava passar uma propriedade do componente filho para o pai
```js
const DarthVader = ({ onScream }) =>{
  <Luke onScream='Nooooooo!!!!'/>
}
```
```js
const handleScream = useCallback((phrase) =>{
  console.log(phrase);
},[])

<DarthVader onScream={handleScream} />
```
Até ai ia muito bem até que eu precisasse passar uma propriedade do filho do filho para o pai, aqui ja teremos que passar por um filho que não vai fazer nada com a informação, ou seja, ele nem deveria saber desta propriedade.

```js
const Lea = ({ onPray }) =>{
  <KyloRen onPray='Vou terminar o que você começou!!!!'/>
}
```
```js

const DarthVader = ({onPray}) =>{
  <Lea onPray />
}
```

```js
const handlePray = useCallback((phrase) =>{
  console.log(phrase);
},[])

<DarthVader onPray={handlePray} />
```

Ainda que no exemplo temos apenas uma propriedade, quando lidamos com componentes mais complexos, como Jar Jar Binks ( hahahahahaha mentira), existem muitas propriedades e algumas precisam vir de outro componente que nem esta na mesma página ou está em outro componente a passagem de propriedades vai se tornando cada vez mais complexa e um código mais sujo.

Para resolver esta situação a implementação do Context API resolveu estes problemas e tornaram o código mais limpo! 

## Conclusão

## Conversão dos exemplos para algo mais genérico.


