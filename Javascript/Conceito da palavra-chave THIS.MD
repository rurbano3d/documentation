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
