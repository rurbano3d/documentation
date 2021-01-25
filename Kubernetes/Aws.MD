# AWS

## Prerequisitos para este projeto
- 4 máquinas com 2 processadores , 4 Gb de memória e 40GB de armazenamento.
- 1 domínio
- Sistema operacional Ubuntu Server 16

## VPC
Virtual private cloud é uma rede virtual privada que é um serviço da Amazon que permite criar redes virtuais. Quando criamos uma maquina virtual ela é inserida dentro da rede virtual.

As VPC possuem subnets que serve para

Para acessar esta maquina virtual pela internet precisamos adicionar um *Internet Gateway* (Network ACL) na VPC.

## EC2
Aqui montamos nossas intâncias configurando nossas maquinas virtuais.

### Passos
1) Executamos a intâncias.

2) Escolher uma AMI (Amazon Machine Image).
  Procuramos qual o sistema operacional que será executado nestas intâncias.
  
3) Escolher o tipo de instância
  Utilizando qual é o requisito da maquina virtual escolhemos qual familia se adequa melhor.

4) Configurar os detalhes da intância
  Number of instances: 4
  Network: coloca a VPC
  
  Em Advanced Details
    Você pode utilizar o User data para colocar informações para executar assim que as maquinas forem criadas. Como por exemplo o Código para instalar o Docker.
  
5) Adicionar armazenamento
  Size: 40 GB
  Volume Type : Magnetic (é mais barato)

6) Adicionar Tags
  key: Name
  Value: rancher-

7) Configurar o Grupo de segurança
  É o firewall da intância.
  Security group name: rancher-kubernetes
  Description: rancher-kubernetes-created-date******
  Type: All traffic
  
8) Informações do lançamento da intância

9) Lançamento
  Create a new key pair
  Key pair name: rancher-kubernetes
  
  Download Key Pair
  
  No terminal execute um chmod 600 rancher-kubernetes.pem, pois preciso mudar a permissão dela para depois conectar na instância.
 
10) Lançar.
  
![launch](assets/Captura%20de%20tela%20de%202021-01-25%2013-13-57.png) 

### Para conectar na sua instâcia via terminal
Pega o IP publico dela.Aqui no exemplo vai ser 0.0.0.0

```shell
ssh -i rancher-kubernetes.pem ubuntu@0.0.0.0

//acessou
sudo su //para acessar o root da maquina
```

## Código para instalar o Docker

``` shell
sudo su
curl https://releases.rancher.com/install-docker/19.03.sh|sh
usemod -aG docker ubuntu
```
