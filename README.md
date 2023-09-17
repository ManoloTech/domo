# DOMO
Repositorio básico para desplegar el entorno de domótica con Docker Compose

## Arquitectura
![alt text](https://github.com/ManoloTech/domo/blob/main/images/arch.png)

## Instalar docker

```
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg
echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update

sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

## Desplegar Monitoring
* Nos movemos a 01monitoring
* Copiar los archivos de example-configs a la raiz de 01monitoring
* Editar env.influxdb y añadir las credenciales
* Editar telegraf.conf y añadir las credenciales
* ```sudo docker compose up -d```
* Las credenciales de InfluxDB serán las que tenemos configuradas en el env.influxdb
* Las credenciales de Grafana son admin:admin

## Desplegar HomeAssistant
* Nos movemos a 02homeassistant
* ```sudo docker compose up -d```
* Añadir las credenciales a example-configs/homeassistant/configuration.yaml
* Copiar example-configs/homeassistant/configuration.yaml al volumen creado con docker compose
* Copiar example-configs/zigbe2mqtt/configuration.yaml al volumen creado con docker compose
* Reiniciamos los servicios ```sudo docker compose restart```
* Las credenciales de Home Assistant se configuran al acceder por primera vez
* Las credenciales de EMQX son admin:public

### Habilitar HACS

```
cd /var/lib/docker/volumes/02homeassistant_config_homeassistant/_data/
wget -O - https://get.hacs.xyz | bash -
```

## Desplegar Omada
* Nos movemos a 03omada
* ```sudo docker compose up -d```

## Desplegar Utils
* Nos movemos a 04utils
* ```sudo docker compose up -d```

### Grafana Dashboards
* Docker: 17020
* System: 15650