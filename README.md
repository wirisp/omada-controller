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

```
sudo apt-get update
```

```
sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```

```
sudo mkdir -m 0755 -p /etc/apt/keyrings
```

```
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

```
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

```
 sudo apt-get update
 ```
 
 ```
 sudo chmod a+r /etc/apt/keyrings/docker.gpg
 sudo apt-get update
 ```
 
 ```
 sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
 ```
 
 ```
 sudo curl -L "https://github.com/docker/compose/releases/download/v2.0.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
 ```
 
 ```
 sudo chmod +x /usr/local/bin/docker-compose
 ```
 
```
mkdir omada
cd omada
wget https://raw.githubusercontent.com/wirisp/omada-controller/master/docker-compose.yml
docker-compose up -d
```
- Usar la ultima version cambiando en docker-compose.yml a latest la version

# Aunque aparezca healty ir a `https://IP:8043`
- La instalacion se puede usar en conjunto con el controlador unifi y no interfieren los puertos, yo la realize usando docker y portainer


### Environment variables variables del sistema
Si algun puerto se encuentra en uso, podemos cambiarlo de acuerdo a la tabla

| Environment variable | Default | Possible values | Description |
| --- | --- | --- | --- |
| HTTPPORT | `8080` | Port from `1025` to `65535` | Internal HTTP port, useful for redirection |
| HTTPSPORT | `8043` | Port from `1025` to `65535` | Internal HTTPS port, useful for redirection |

### Notas

- It is useful to change the HTTPSPORT as Omada redirects you to its internal `HTTPSPORT`.
So if you want to run the container with `-p 8000:8000` for the HTTPS port, you need to set `HTTPSPORT=8000`.
- From [TP Link Omada's FAQ](https://www.tp-link.com/us/support/faq/865), Omada controller uses the ports:
    - 8043 (TCP) for https
    - 8088 (TCP) for http
    - 27001 (UDP) for controller discovery
    - 27002 (TCP) for controller searching
    - ~27017 (TCP) for mongo DB server~ (internally)
    - 29810 (UDP) for EAP discovery
    - 29811 (TCP) for EAP management
    - 29812 (TCP) for EAP adoption
    - 29813 (TCP) for EAP upgrading

## TODOs

- [ ] Healthcheck
- [ ] Instructions with proxy and port redirection
