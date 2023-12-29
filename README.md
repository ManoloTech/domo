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
* Copiamos los archivos de example-configs a la raiz de 01monitoring
* Editamos env.influxdb y añadir las credenciales
* Editamos telegraf.conf y añadir las credenciales
* ```sudo docker compose up -d```
* Las credenciales de InfluxDB serán las que tenemos configuradas en el env.influxdb
* Las credenciales de Grafana son admin:admin

## Desplegar HomeAssistant
* Nos movemos a 02homeassistant
* Copiamos /example-configs/esphome/env.esphome a la raiz de 02homeassistant
* Editamos env.esphome y añadimos las credenciales 
* ```sudo docker compose up -d```
* Añadimos las credenciales a example-configs/homeassistant/configuration.yaml
* Copiamos example-configs/homeassistant/configuration.yaml al volumen creado con docker compose
* Copiamos example-configs/zigbe2mqtt/configuration.yaml al volumen creado con docker compose
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

### 
Bootstrap CA

Añadimos lo siguiente al provisioner:
```
                               "claims": {
                                    "maxTLSCertDuration": "9480h",
                                    "defaultTLSCertDuration": "9480h"
                                }
```

Obtenemos el fingerprint the la Root CA generada:
```
openssl x509 -noout -fingerprint -sha256 -inform pem -in root_ca.crt 
```
Configuramos el cliente de step ca con la URL y el fingerprint:

```
step ca bootstrap --ca-url https://ca.manolotech.com:9000 --fingerprint B098FFF65100BE77B888F16E22053F65ABBB882A73F8FAC25E60F4327B36FACD
```

### Otros
Alarmo
https://github.com/nielsfaber/alarmo

Mushroom
https://github.com/piitaya/lovelace-mushroom

Custom State: {{ states("sensor.sensor_temperatura_humedad_01_temperature") }}ºC

Mini Graph Card
https://github.com/kalkih/mini-graph-card

