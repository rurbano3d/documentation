# Closures (Fechamentos)

Closures é sobre como preservar o contexto e principalmente como um função interna pode manter o contexto de seu pai.
```js
  function setTestValue(value){
    var firstNum = value || 2;
    
    return (secondNum) => {
      if(firstNum > secondNum){
        return firstNum;
      }else if(firstNum < secondNum){
        return secondNum;
      }else{
        return '=';
      }
    }
  }
  
  var theNumberExaminer = setTestValue(6);
  var result = theNumberExaminer(2);
  
  console.log(result); // 6
```
A função anônima interna é retornada da chamada da função setTestValue e, com ela, o contexto de execução de sua função pai. Isso permite que a função anônima tenha acesso ao valor de firstNum.

Outro exemplo abaixo sobre *Closures*
```js
  function myClosedObject (){
    var privateValue = 5;

    function privateFunc (){
      privateValue *= 2;
      return privateValue ;
    }

    this.publicFunc = function(){
      return privateFunc();
    };
  }

  var firstObj = new myClosedObject ();
  console.log(firstObj.publicFunc()); // 10
  console.log(firstObj.publicFunc()); // 20

```
