# Ionic 
## Angular

### Capturar, salvar localmente e subir para as nuvens

Conteudo extraído de https://www.youtube.com/watch?v=4XiBXFDXesg&t=942s

#### Plugins
```npm
@ionic-native/camera
@ionic-native/file
@ionic-native/ionic-webview
@ionic/storage
```


Adicione os plugins no cordova
```npm
ionic cordova plugin add cordova-plugin-camera
ionic cordova plugin add cordova-plugin-file
ionic cordova plugin add cordova-plugin-ionic-webview
ionic cordova plugin add cordova-sqlite-storage
```

No app.module.ts
```ts
import {IonicStorageModule} from '@ionic/storage';
import {HttpCientModule} from '@angulat/common/http';

import {Camera} from '@ionic-native/Camera/ngx';
import {File} from '@ionic-native/File/ngx';
import {WebView} from '@ionic-native/ionic-webview/ngx';

@NgModule({
  //.....
  imports:[IonicStorageModule.forRoot(), HttpClientModule],
  providers:[Camera, File, Webview]
  //....
})
```

HTML
```html
<ion-list>
  <ion-item *ngFor="let img pg images; index as pos">
    <ion-thumbnail slot="start">
      <ion-img [src]="img.path"></ion-img>
    </ion-thumbnail>
    
    <ion-label>{{ img.name }}</ion-label>
    
    <ion-button slot="end" fill="clear" (click)="startUpload(img)">
      <ion-icon slot="icon-only" name="cloud-upload"></ion-icon>
    </ion-button>
    
    <ion-button slot="end" fill="clear" (click)="delete(img)">
      <ion-icon slot="icon-only" name="trash"></ion-icon>
    </ion-button>
  </ion-item>
</ion-list>

<ion-button fill="clear" expand="full" color="light" (click)="selectImage()">
  <ion-icon name="camera" slot="start"></ion-icon>
    Select Image
</ion-button>
```

Lógica
```ts

```
  
