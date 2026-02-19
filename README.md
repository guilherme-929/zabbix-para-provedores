

Instalação do Zabbix em docker
# Instalando dependencias
apt-get update && apt-get upgrade -y && apt-get install curl wget htop unzip sudo rsync lftp sudo -y

# Instalação do docker

curl -fsSL https://get.docker.com | sh

# Instalação docker compose

curl -L "https://github.com/docker/compose/releases/download/v2.0.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

# Permissão na pasta 

chmod +x /usr/local/bin/docker-compose

# Siga todo o passo a passo do E-book.
