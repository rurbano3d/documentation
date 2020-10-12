# Material Icons no VSCode.

Vamos personalizar nossas pastas utilizando a  extensão [Material Icons](https://marketplace.visualstudio.com/items?itemName=PKief.material-icon-theme)

Em *settings.json* adicione.
```json
//Pastas
"material-icon-theme.folders.associations":{
  "nome_da_pasta_no_seu_projeto":"o-icone-que-escolher-do-material-icon",
}

//Arquivos
"material-icon-theme.files.associations":{
  "nome_mais_a_extensão_do_arquivo_no_seu_projeto":"o-icone-que-escolher-do-material-icon",
}
```

Exemplo:
```json
"material-icon-theme.folders.associations":{
  "infra":"app",
  "entities":"class",
  "schemas":"class",
  "typeorm":"database",
  "repositories":"mappings",
  "http":"container",
  "migrations":"tools",
  "modules":"components",
  "implementations":"core",
  "dtos":"typescript",
  "fakes":"mock"
},

"material-icon-theme.files.associations":{
  "ormconfig.json":"database",
  "tsconfig.json":"tune"
}

```
