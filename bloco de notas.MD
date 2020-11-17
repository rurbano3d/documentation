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

## Infinite Scroll na mão
```ts
const scrollRef = useRef<HTMLInputElement>(null);

useEffect(() => {
    if (scrollRef.current) {
      scrollRef.current.addEventListener('scroll', () => {
        const Scroll = scrollRef.current;
        if (Scroll && Scroll.scrollTop + Scroll.clientHeight >= Scroll.scrollHeight) {
          console.log('aqui');
          
        }
      });
    }

    console.log(scrollRef.current);
  }, []);

```

## Mover Scroll para o início

```js
 const scrollRef = createRef<HTMLDivElement>();
  
const updateScroll = useCallback(() => {
    if (scrollRef.current) {
      scrollRef.current.scrollTo({ left: 0 });
    }
  }, [scrollRef]);
```
