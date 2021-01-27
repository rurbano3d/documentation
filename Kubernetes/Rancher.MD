# Rancher

è um orquestrador de kubernetes.

```shell
 docker run -d --name rancher --restart=unless-stopped -v /opt/rancher:/var/lib/rancher  -p 80:80 -p 443:443 rancher/rancher:v2.4.3
```

no comando *-v /opt/rancher:/var/lib/rancher estamos persistindo os dados, para quando este cluste morrer e subir outro as informações deles continuam armazenadas.

## Instalar kubernetes

Vamos utilizar um agente do Rancher para criar os kubernetes clusters em cada maquina (k8s-1m k8s-2, k8s-3).

Dentro do rancher > Global > Add Cluster

### Add Cluster

Clica em From existing nodes (Custom)

Cluster Name: Curso
Advanced Options:
 Nginx Ingress : disabled (nos iremos utilizar outro nginx que é o traefic)
 
 Next
 
 ### Cluster Options
 Node Options: check etcd, control plane e worker
 
 Etcd é o banco de dados do Kubernetes
 Control Plane é o controlador do Kubernetes, tem apis, scheduler
 Worker são componentes que vão somente rodar aplicações
 
 Clique em Show advanced options
 Node name: k8s-1
 
 E copiamos o código gerado para acionar nas maquinas k8s, usamos o mesmo código para todas e so trocamos o Node Name.
 
 ## Interface do Rancher
 Global mostra os Clusters criados. Se eu clicar no nome do Cluster ele abre outro menu com informações de performance e em Node vc analisa cada um deles separadamente.
 
 
