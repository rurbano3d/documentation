#### obs: Sempre com a temática star wars, senhor dos anéis, etc.
* Falar de todos os métodos de array, com string e objetos.

* Mostrar o conceito do useCallback.

* Mostrar diversas formas de armazenar um array no storage, exemplo abaixo
```js
const addToCart = useCallback(
    async product => {
      const productExists = products.find(item => item.id === product.id);
      if (productExists) {
        setProducts(
          products.map(p =>
            p.id === product.id ? { ...product, quantity: p.quantity + 1 } : p,
          ),
        );
      } else {
        setProducts([...products, { ...product, quantity: 1 }]);
      }
      await AsyncStorage.setItem(
        '@GoMarketPlace:products',
        JSON.stringify(product),
      );
    },
    [products],
  );
```
