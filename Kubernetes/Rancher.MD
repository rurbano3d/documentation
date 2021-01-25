# Rancher

è um orquestrador de kubernetes.

```shell
 docker run -d --name rancher --restart=unless-stopped -v /opt/rancher:/var/lib/rancher  -p 80:80 -p 443:443 rancher/rancher:v2.4.3
```

no comando *-v /opt/rancher:/var/lib/rancher estamos persistindo os dados, para quando este cluste morrer e subir outro as informações deles continuam armazenadas.

