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


# Aunque aparezca healty ir a `https://IP:8043`
- La instalacion se puede usar en conjunto con el controlador unifi y no interfieren los puertos, yo la realize usando docker y portainer
