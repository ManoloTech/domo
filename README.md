# domo-portainer-base
Repositorio básico para desplegar el entorno con portainer y monitoring


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

## Desplegar HomeAssistant

## Desplegar Omada

## Desplegar Utils

### Habilitar HACS

```
cd /var/lib/docker/volumes/02homeassistant_config_homeassistant/_data/
wget -O - https://get.hacs.xyz | bash -
```

### Grafana Dashboards

* Docker: 17020
* System: 15650