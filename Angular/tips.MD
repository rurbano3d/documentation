## Acessar uma função dentro de um componente filho.

```ts
  import { ViewChild } from '@angular/core';
  
  import { NomeDoComponente } from '../../components/PastaDoComponente/componente.componet';
  
  @ViewChild(NomeDoComponente)
  nomeDoComponente: NomeDoComponente;
  
  this.nomeDoComponente.função();
```
