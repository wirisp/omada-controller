# omada-debian
Instalacion de controlador omada en debian 11

```
wget https://raw.githubusercontent.com/wirisp/omada-debian/main/omada.sh
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

## Instalacion alternativa en Docker

```
docker run -d --name=omada-controller \
-e PUID=1026 \
-e PGID=100 \
-e TZ=Europe/Bucharest \
-e MANAGE_HTTP_PORT=8088 \
-e MANAGE_HTTPS_PORT=8043 \
-e PORTAL_HTTP_PORT=8088 \
-e PORTAL_HTTPS_PORT=8043 \
-e SHOW_SERVER_LOGS=true \
-e SHOW_MONGODB_LOGS=false \
-e SSL_CERT_NAME="tls.crt" \
-e SSL_KEY_NAME="tls.key" \
-v /volume1/docker/omada/data:/opt/tplink/EAPController/data \
-v /volume1/docker/omada/logs:/opt/tplink/EAPController/logs \
-v /volume1/docker/omada/work:/opt/tplink/EAPController/work \
--net host \
--restart always \
mbentley/omada-controller
```

- #Aunque aparezca healty ir a IP:8043
- La instalacion se puede usar en conjunto con el controlador unifi y no interfieren los puertos, yo la realize usando docker y portainer
