# Javascript Modular

## Breve revisão de conceitos de Javascript OOP

É possível criar objetos de várias maneiras em Javascript. ALgumas delas estão baixo.

###### Construtores de tipo de objeto nativo  (native object type constructors)

Essa sixtaxe para criar objetos, com o uso de um constructor de objeto *new Object()* não é tão otimizada, pois o interpretador precisa fazer uma resolução de escopo para determinar se existe um constructor local com o mesmo nome ou não, a fim de criar a cadeia de escopo corretamente.

```js
  var myObj = new Object();
  
  myObj.value = "my first value";
  myObj.method = () =>{
    return this.value;
  };
  console.log(myObj.method())/ //displays "my first value"
```

###### Notação literal de objeto (object literal notation)

Aqui é possível passar vários parâmetros para funções em vez de passar um parâmetro por vez.
```js

 var MyFirstObj = {
    myFirstValue : 2,
    mySecondValue : 5,
    
    addValues: () =>{
      return this.myFirstValue + this.mySecondValue;
    }
 }
 console.log(MyFirstObj.addValues()); //displays 7
```

###### Funções construtoras (constructor functions)
Utilizamos a palavra-chave *new* e podemos criar uma instância desse objeto.

```js
  function MyObjDefinition(){
    var myFirstValue = 2;
    var mySecondValue = 5;
    
    this.addValues = () => {
      return this.myFirstValue + this.mySecondValue;;
    }
  }
  
  var myFirstObj = new MyObjDefinition();
  
  console.log(MyFirstObj.addValues()); //displays 7
```

Ao entendermos que no Javascript tudo é um objeto, até as funções, podemos trasformar este código acima em um objeto estático.

```js
  function MyObjDefinition(){
    MyObjDefinition.myFirstValue = 2;
    MyObjDefinition.mySecondValue = 5;
  }
  
  MyObjDefinition.addValues = () => {
     return this.myFirstValue + this.mySecondValue;;
  }
    
   
  }
  
  MyObjDefinition();
  
  console.log(MyObjDefinition.addValues()); //displays 7
```

Na maioria das vezes utilizamos funções construtoras quando precisamos criar várias instâncias de um objeto. Já notação literal de objeto para empacotar parâmetros (dados) que precisam ser passados para diferentes partes do aplicativo etambém para crição de código modular.
