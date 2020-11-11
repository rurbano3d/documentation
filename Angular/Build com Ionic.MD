# Build com Ionic

## IOS

```shell
  ionic cordova build ios
```

Abre no XCode o projeto e vai em plataforms > ios > Nome.xcworkspace.

Atualize a versão
Verifique o nome do pacote

## Android

```shell
  ionic cordova build android
```

Para gerar um bundle ao invez de um apk
Acesse a pasta plataform > android
```shell
  cd plataform/android
  
  ./gradlew bundle
```

jarsigner -verbose -sigalg SHA1withRSA -digestalg SHA1 -keystore emove.keystore /Volumes/DADOS/Programacao/Angular/Emove/gestao-de-frotas-ionic/platforms/android/app/build/outputs/bundle/release/app.aab alias_name
