# omada-debian
Instalacion de controlador omada en debian 11

```
wget https://raw.githubusercontent.com/wirisp/omada-controller/main/omada.sh
```

```
chmod +x omada.sh
```

```
bash omada.sh
```

_Acceder al controlador por medio de la Ip:8043 u Ip:8088_

## Eliminacion de omada

```
cd /opt/tplink/EAPController
```
```
./uninstall.sh
```

## Instalacion alternativa en Docker 1

``
wget https://raw.githubusercontent.com/wirisp/omada-controller/master/docker-compose.yml
docker-compose up -d
```


- #Aunque aparezca healty ir a `https://IP:8043`
- La instalacion se puede usar en conjunto con el controlador unifi y no interfieren los puertos, yo la realize usando docker y portainer
