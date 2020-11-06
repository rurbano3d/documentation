Errado
```js
 getThem(){
    const list1 = new ArrayList();
    for each( let x in theList){
        if(x[0] == 4){
            list1.add(x);
        }
    }
    return list1;
 }
```
Correto
```js
getFlaggedCells(){
    const flaggedCells = new Arraylist();
    for each (let cell in gameBoard){
        if(cell.isFlagged()){
            flaggedCells.add(cell);
        }
    }
    return flaggedCells;
}
```

Errado
```js
    copyChars(a1[], a2[]){
        for (int i = 0; i < a1.length; i++){
            a2[i] = a1[i];
        }
    }
```

Correto
```js
    copyChars(source[], destination[]){
        for (int i = 0; i < source.length; i++){
            destination[i] = source[i];
        }
    }
```
