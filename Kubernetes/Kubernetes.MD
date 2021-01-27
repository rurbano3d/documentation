# Dentro do Kubernetes

## Instalação do Kubectl

É a linha de comando para trabalharmos com kubernetes.

Acesse a maquna que esta instalado o Rancher. E instale o kubectl

```shell
$ sudo apt-get update && sudo apt-get install -y apt-transport-https gnupg2
$ curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
$ echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee -a /etc/apt/sources.list.d/kubernetes.list
$ sudo apt-get update
$ sudo apt-get install -y kubectl
```

### Agora precisamos pegar as configurações do kubernetes do rancher e colocar na maquina.

Para pegar no Rancher acesse o cluster desejado e no topo direito vc encontra um botão Kubeconfig File e copiei o conteudo gerado.

Na maquina vá para raiz do ubuntu, se tiver com sudo su basta digitar exit, caso tenha acessado a maquina agora vc ja esta na raiz.

Crie uma nova pasta
```shell
mkdir -p ~/.kube
```

crie um arquivo e cole as configurações que pegou no Rancher.
```shell
vi ~/.kube/config
```


Glossário
```kubectl get nodes``` pega todos os nodes
```kubectl get pods -n kube-system``` pega todos os pods do namespace kube-system
