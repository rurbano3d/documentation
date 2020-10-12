#### Objects
```js

    fellowshipMember.id = uuid();
    fellowshipMember.name = 'Sam';
    fellowshipMember.jobFunction = 'Master of Focus';
    
    //Pode ser substituído por
    
    Object.assign(fellowshipMember, { id: uuid(), name:'Sam', jobFunction:'Master of Focus' });
    
```

#### Arrays

```js
// Forma 01
if (data.length > 0) {
  console.log("Possui informação");
}

//Forma 02
if (!!data.length) {
  console.log("Possui informação");
}

// O símbolo ! converte a expressão para um valor Booleano.
// Quando utilizamos apenas um sinal ! ele verifica se a
// expressão retorna :[false, NaN, undefined, null, "", 0]
// Quando utilizamos dois sinais !!, se existir informação
// ele retorna TRUE, caso contrário FALSE.
```
### Async
```js
// Desta vez veremos como utilizar .map e async/await as famosas Promises.

const dataParse = data.map(async (item) => {
  const info = await infoBD(item.id);
  return {
    info,
    item,
  };
});

Promise.all(dataParse).then((result) => console.log(result));

//Como estamos mapeando e obtendo informação assíncrona
//a resposta sempre será um Promise, portanto utilizamos
//Promise.all para resolver todas as promessas.
```

### Function Pattern
```js
function Nazgul(name) {
  function search() {
    console.log(name + "is searching");
  }

  return {
    name: name,
    attack: function () {
      console.log(this.name + " is attacking");
    },
  };
}
// Instâncio Nazgul
let nazgul = Nazgul("Witch King");

//nazgul.name e nazgul.attack retornam as informações
//nazgul.search retorna erro, pois ela esta privada. Para torna-la publica, você precisa retorná-la.

return {
  name: name,
  attack: function () {
    console.log(this.name + " is attacking");
  },
  search: search,
};
//Todas as funções estão publicas.

```
