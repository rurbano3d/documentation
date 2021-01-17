O react utiliza a imutabilidade para tratar o que vai re-renderizar na tela, ou seja, quando temos um elemento ou estado que foi alterado o React consegue analisar a referência deste elemento ou estado, e se ele for alterada é renderizado novamente.

Otimo, então existe um por que para o React utilizar a imutabilidade, mas como ela funciona?

Chamarei daqui pra frente um elemento ou estado de objeto.

Um objeto mutável altera seu valor sem precisar alterar sua referência, por exemplo:

Um objeto foi criado na referência de memória 158765646 e seu estado (valor) é 'Luke Skywalker'.
```js
const jedi = 'Luke Skywalker';
```

Na memoria do seu navegador existe no espaço 158765646 uma informação 'Luke Skywalker', para a nossa aplicação este número 158765646 é referênciado como jedi. Toda vez que chamar a constante jedi na aplicação estamos chamando o endereço de memória 158765646.

Note que se precisar alterar este valor utilizando o conceito de objeto mutável ficaria assim:
```js
const jedi = 'Obi Wan';
```

O que fizemos foi que no endereço de memoria 158765646 a informação que antes era 'Luke Skywalker' agora é 'Obi Wan', como o endereço de memória permanece o mesmo o React não consegue identificar que houve uma mudança de referência portanto não é renderizado novamente.

Agora vamos tratar a mesma situação utilizando um objeto imutável.

Temos um ojeto criado na referência de memória 158765646 e seu estado (valor) é 'Luke Skywalker'.
```js
const jedi = 'Luke Skywalker';
```

Porém como ela é imutável não podemos altera-la como acima no exemplo de objeto mutável, é necessário criar um novo objeto. 
Para isso entra em ação uma técnica chamada COW ([Copy-on-write](https://en.wikipedia.org/wiki/Copy-on-write)).

Ao utilizar o setState (setJedi) do React é criado uma nova cópia do objeto. 

```js
const setJedi('Obi Wan');
```

Agora no endereço de memória 158765646 ainda possuimos a informação 'Luke Skywalker' e em outro endereço 58746488 temos a informação 'Obi Wan'. Potanto temos dois endereços de memórias ao invez de ter apenas um como em objeto mutável. O que o React faz é mudar a referência Jedi para o novo objeto criado no endereço de memoria 58746488 com a informação nova e desta forma o react consegue encontrar a mudança e renderizar novamente a tela com esta alteração.

Objeto mutável você altera seu estado sem alterar sua referência.</br>
Objeto Imutável você cria um novo objeto com a alteração de estado e aponta a referência antiga para este novo objeto.



