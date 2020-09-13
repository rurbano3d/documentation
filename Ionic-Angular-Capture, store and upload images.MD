# Ionic 
## Angular

### Capturar, salvar localmente e subir para as nuvens

Conteudo extraído de https://www.youtube.com/watch?v=4XiBXFDXesg&t=942s

O que vamos fazer:
  * Capture imagens usando a câmera ou biblioteca de fotos
  * Armazene arquivos de imagem dentro de seu aplicativo Ionic 4
 * Faça upload de arquivos de seu caminho local usando uma solicitação POST

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
    
    <ion-button slot="end" fill="clear" (click)="delete(img, pos)">
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

Gerando uma página pelo Ionic, obtemos o código abaixo:
home.page.ts

```ts
import { Component, OnInit } from '@angular/core;

@Component({
  selector: 'app-home',
  templateUrl: 'home.page.hmtl',
  stylesUrls: ['home.page.scss'],
  })
  
  export class HomePage implements OnInit{
    constructor();
    
    ngOnInit(){}
  }
```

Importações necessárias 
```ts
import {Component, OnInit, ChangeDetectorRef} from @angular/core;
import { Camera, CameraOptions, PictureSourceTyoe} from '@ionic-native/Camera/ngx'
import { ActionSheetController, Platform } from @ionic/angular
// Action Sheet Controller é uma caixa de diálogo que exibe um conjunto de opções
import { File, FileEntry } from '@ionic-native/File/ngx';
import {HttpClient} from @angular/common/http';
import {WebView} from '@ionic-native/ionic-webview/ngx';
import { Storage } from '@ionix/storage';
import { finalize } from 'rxjs/operators';

const STORAGE_KEY = 'my_images'; 

//constructor
constructor(
  private camera: Camera,
  private file: File,
  private http: HttpClient,
  private webview: WebView,
  private actionSheetController: ActionSheetController,
  private toastController: ToastController,
  private storage: Storage,
  private plt: Platform,
  private loadingController: LoadingController,
  private ref: ChangeDetectorRef, 
  private filePath: FilePath,
)



```

Array para armazenar as imagens
```ts
  images=[],
```

Se a platforma estiver pronta iniciaremos nossa função para carregar os dados do Storage.
```ts

ngOninit(){
  this.plt.ready().then(() -> {
    this.loadStoredImages();
  });
}
```

Pega imagens do Storage.

```js 
loadStoredImage(){
  // em STORAGE_KEY contém o nome de um arquivo,tratamos como um referência.Por ex: img.jpg, 
  this.storage.get(STORAGE_KEY).then(images => {
    if(images){
      let arr = JSON.parse(images);
      this.images=[];
      //Portanto para cada entrada precisamos resolver o nome para a URL local
      //do nosso aplicativo, que é adicionado em filePath
      for (let img of arr) {
        let filePath = this.file.dataDirectory + img;
        let resPath = this.pathForImage(filePath);
        this.images.push({name: img, path: resPath, filePath: filePath });
      }
    }
  });
}
```

Para exibir ou manipular uma imagem precisamos converter o caminho.
```ts
pathForImage(img){
  if(img === null){
    return '';
  } else {
    // this.webview.convertFileSrc resolve um file://url para uma url que o WebView entende.
    let converted = this.webview.convertFileSrc(img);
    return converted;
  }
}
```

* Porque temos que resolver a URL de uma imagem?

    Quando capturamos uma imagem e movemos para uma pasta do nosso aplicativo, poderiamos armazenar toda a url para este arquivo. O problema é que algumas partes da URL pode mudar se o sistema operacional limpar algum cache e mover as coisas de modo que nosso arquivo ainda estará lá, mas o caminho que armazenamos não está mais correto. Portanto vamos apenas armazenar o nome do arquivo e então podemos utilizar o WebView.convertFileSrc (https://ionicframework.com/docs/core-concepts/webview), para converter o FileSource.

    No IOS você não tem permissão para utilizar algo que comece com file://, por isso o WebView.convertFileSrc converte para uma URL especial que você manipular e exibir.

    Também funciona no ANDROID

    Dica: não armazene o caminho errado e converta a URL.
    
    Conclusão: Para exibir ou manipular uma imagem no seu aplicativo o uso da conversão é essencial. Entretanto para subir sua imagem para as nuvens precisamos utilizar o FileReader e o caminho convertido não. POrfunciona para ele, por isso tambem enviamos o caminho "puro".
    ```ts
    let filePath = this.file.dataDirectory + img;
    ```
    
Selecionar as imagens

```js 
async selectImages(){
  const actionSheet = await this.actionSheetController.create({
    header: "Select Image Source",
    buttons:[{
      text:'Load form Library',
      handler: () ->{
        this.takePicture(this.camera.PictureSourceType.PHOTOLIBRARY);
      }
    },
    {
      text:'Use Camera',
      handler: () => {
        this.takePicture(this.camera.PictureSourceTyoe.CAMERA);
      }
    },
    {
      text:'Cancel,
      role:'cancel'
    }
    ]
  });
  await actionSheet.present();
}
```
Capturar a imagem
```ts
takePicture(sourceType: PictureSourceType) {
 var options: CameraOptions = {
  quality: 100,
  sourceType: sourceType,
  saveToPhotoAlbum: false,
  correctOrientation: true
 };
 
 this.camera.getPicture(options).then(imagePath => {
  var currentName = imagePath.substr(imagePath.lastIndexOf('/') + 1;
  var correctPath = imagePath.substr(0, imagePath.lastIndexOf('/') + 1;
  this.copyFileToLocalDir(correctPath, currentName, this.createFileName());
 });
}
```
* Normalmente utilizamos a versão base64 de uma string. O problema é que se você armazenar muitas imagens codificadas em base64 no banco de dados pode ficar muito grande, então, para melhorar isso, simplesmente queremos armazenar a referência. Por isso estamos utilizando o FILE_URI real da imagem.

Dar um nome único a imagem
```ts
createFileName(){
 var d = new Date(),
     n = d.getTime(),
     newFileName = n + ".jpg";
 return newFileName;
}
```
Copiar a imagem para nosso diretório de dados.
```ts
copyFileToLocalDir(namePath, currentName, newFileName){
 this.file.copyFile(namePath, currentName, this.file.dataDirectory, newFileName).then(success =>{
  this.updateStoredImages(newFileName);
 }, error => {
  console.log('Error while storing file.');
 });
}
```

Armazenamento local da referência
```ts
updateStoredImages(name){
 this.storage.get(STORAGE_KEY).then(images => {
  let arr = JSON.parse(images);
  if(!arr) {
   let newImages = [name];
   this.storage.set(STORAGE_KEY), JSON.stringify(newImages));
  } else {
   arr.push(name);
   this.storage.set(STORAGE_KEY, JSON.stringify(arr));
  }
  
  let filePath = this.file.dataDirectory + name;
  let resPath = this.pathForImage(filePath);
  
  let newEntry = {
   name: name,
   path: resPath,
   filePath: filePath
  }
  
  this.images = [newEntry, ...this.images];
  this.ref.detectChanges(); //trigger change detection cycle
 });
}
```

Deletar imagem
 * Remova o objeto de nosso images array local
 * Remova o item do armazenamento
 * Remova o arquivo real da pasta do nosso aplicativo

```ts
deleteImage(imgEntry, position){
 this.images.splice(position,1);
 
 this.storage.get(STORAGE_KEY).then(images =>{
  let arr = JSON.parse(images);
  let filtered = arr.filter(name => name != imgEntry.name);
  this.storage.set(STORAGE_KEY, JSON.stringify(filteres)):
  
  var correctPath = imgEntry.filePath.substr(0, imgEntry.filePath.lastIndexOf('/') + 1);
  
  this.file.removeFile(correctPath, imgEntry.name).then(res =>{
   console.log('File removed');
  });
 });
}
```


 
