# Rodando a aplicação em Docker Container

Instale o Git e Docker-compose
Dê permissão para o docker-compose e depois copie ele para o repositório bin para virar um executavel.

```shell
chmod +x /usr/local/bin/docker-compose

ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose

docker-compose --version
```

Clone o repositório.

## Docker stand-alone

Utilizando as configurações dentro do *Dockerfile* buildamos o container.
```shell
docker build -t <nome-do-usuario>/redis:devops .
```

Agora vamos rodar este container.
```shell
docker run -d --name redis -p 6379:6379 <nome-do-usuario>/redis:devops 
```
## Docker Compose
Agora vamos subir nossos serviços todos de uma vez utilizando o docker-compose, por meio do *docker-compose.yml*.
É importante buildar todos os containers antes de executar o docker-compose. 

```shell
docker-compose -f docker-compose.yml up -d

// caso queira matar todos os containers 
docker-compose down
```







