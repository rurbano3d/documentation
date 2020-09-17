# Package and scope ( Encapsulamento e escopo)

Quando criamos uma variável dentro da função usando *var* estamos criando uma variável **privada**, pois o escopo da variável está contido na função, não conseguindo acessar ela fora da função. 
Se utilizarmos uma função construtora, que cria uma instância  do objeto, também não acessamos a variável **privada** fora da função.

```js
  function simpleFunc(){
    var firstValue = 1;
    var secondValue = 2;
    this.instanceValue = 100;
    
    for (var i=0; i<50; i++){
      var thirdValues = firstValue * secondValue + i;
    }
    console.log(thirdValue) // 52
  }
  
  simpleFunc();
  
  console.log(simpleFunc.firstValue); //undefined
  console.log(simpleFunc.instanceValue); //undefined
```

Agora utilizando uma função construtora, a unica diferença é que você poderá acessar *instanceValue*, pois criamos uma instância do objeto e *this* se refere à esta instância do objeto.
```js
  function simpleFunc(){
    var firstValue = 1;
    var secondValue = 2;
    this.instanceValue = 100;
    
    for (var i=0; i<50; i++){
      var thirdValues = firstValue * secondValue + i;
    }
    console.log(thirdValue) // 52
  }
  
  var testObj = new simpleFunc();
  
  console.log(testObj.firstValue); //undefined
  console.log(testObj.instanceValue); //100
```

Aqui o erro ocorre porque criamos um **(namespace)** privado dentro da função construtora que está totalmente oculo do mundo externo.
```js
  function simpleFunc(){
    var firstValue = 1;
    
    (function(){
      var secondValue = 2;
      this.instanceValue = 100;
      
      console.log(firstValue); // shows 1
    })();
    
//console.log(secondValue); //produces an error

var testObj = new simpleFunc();
console.log(testObj.instanceValue); // undefined
}
```

Agora se quisermos criar uma função construtora que forneça métodos públicos, para que possa acessar variáveis privadas usando esses métodos ( Método Privilegido).Temos:

```js
  function simpleFunc(){
    var privateValue = 1;
    
    this.readPrivateValue = () =>{
      return privateValue;
    }
  }  
  
  var testObj = new simpleFunc();
  console.log(testObj.readPrivateValue()); // 1
```
