# CSS

## Overflow
 Uma propriedade que trata elementos filhos que transborda a visualização no elemento pai.
 
 ```css
 overflow:hidden
 ```
 Esconde todo elemento que tranborda do elemente pai
 
 Trabalhando com *oveflow:hidden* e *position:absolute*
 
```css
.elemento_pai{
  position:relative;
  overflow:hidden;
}

.elemento_filho{
  position:absolute;
}
```
