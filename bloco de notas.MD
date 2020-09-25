## Reduce

Objetivo: Pegar a quantidade de produtos em um array e multiplicar pelo valor.
Então você :
  * percorrer um array 
  * multiplica as propriedades(price, quantity) dos elementos( cada produto) do array (products)
```js
 const total = products.reduce((accumulator, product) => {
      const productSubTotal = product.price * product.quantity;

      return accumulator + productSubTotal;
    }, 0);
```
* *productSubtotal* da o resultado da multiplicação de cada produto em individual.
* *accumulator* da o resultado da soma de todos os *productSubtotal*.


Entender conceito do reduce. Utilizar ele em situações extremas.
