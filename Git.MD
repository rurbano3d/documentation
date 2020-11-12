# GIT

## Criar e mudar para um novo Branch

```
git checkout -b nomeDoBranch
```

## Merge com outro branch

Exemplo para dar merge do branch *dev* para o *master*
```
git checkout master

git merge dev
```

## Pegar hash dos commits
```
git log
```
Para sair aperte *q*

## Desfazer um commit
Peque o hash do commit da ultima versão que esteja segura utilizando o *git log*
```
git reset --hard 66128fcc3985012db216dccfc7b6ed14a99f6751
```
