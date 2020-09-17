#  Palavra-chave *this*
*this* é simplesmente uma referência a um objeto.

Quando utilizada em um função construtora simples
```js
function Person(){
  this.name = "Rodrigo".
  this.job = "Desenvolvedor de Software
}

console.log(window.name) // "Rodrigo"
console.log(window.job) // "Desenvolvedor de Software"
```
A palavra-chave *this* tem um contexto global. Portanto dentro da função Person, *this* se refere ao objeto window (se o código for executado em um navegador).

Agora se utilizarmos assim.
```js
function CreatePerson (personData){
  this.name = personData.Name;
  this.job = personData.Job;
}
var personOneData = {
  Name: "Rodrigo",
  Job: "Desenvolvedor de Software"
}

var firstPerson = new CreatePerson(personOneData);

console.log(firstPerson.name) // "Rodrigo"
console.log(firstPerson.job) // "Desenvolvedor de Software"
```
A palavra-chave *this* se refere à instância firstPerson.

Agora vamos exemplificar três situações.

```js
  var name = "The window global";
  
  var myOwnObject={
    name: "The own object",
    getName: () =>{
      return this.name;
    }
  }
  
  console.log(myOwnObject.getName()); // "The own Object"
```
Neste primeiro exemplo o *this* é referente ao contexto myOwnProject, pois definimos um objeto usando a notação literal que foi atribuído à variável myOwnObject e seu método retorna o valor da propriedade name no objeto.
```js
  var name = "The window global";
  
  var myOwnObject={
    name: "The own object",
    getName: () =>{
      return () =>{
        return this.name;
      } 
    }
  }
  
  console.log(myOwnObject.getName()); // "The window global"
```
Como função mais interna é uma função anônima dentro de outra função anônima, o contexto da função mais interna é diferente do objeto que a hospeda. O *this* está referenciado ao contexto global.

```js
  var name = "The window global";
  
  var myOwnObject={
    name: "The own object",
    getName: () =>{
    var that = this;
      return () =>{
        return that.name;
      } 
    }
  }
  
  console.log(myOwnObject.getName()); // "The own object"
```

Aqui criamos um contexto dentro da primeira função interna que faz referência ao nosso obejto e, em seguida, a função mais interna pode acessar esse contexto.

Pode ser desafiador descobrir a que contexto o *this* se refere às vezes, mas com prática e mais experiência você se tornará melhor nisso.
