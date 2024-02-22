# Zabbix Monitoring Solution with Docker Compose

Este projeto configura uma solução completa de monitoramento usando Zabbix, integrado com MySQL para banco de dados, Zabbix Server, Zabbix Frontend, Zabbix Agent e Grafana para visualização de dados, tudo isso gerenciado através do Docker Compose.

## Pré-requisitos

- Docker e Docker Compose instalados no sistema.
- Acesso ao terminal ou linha de comando.
- Conhecimento básico de Docker.

## Configuração

Antes de iniciar, certifique-se de configurar as variáveis de ambiente necessárias. Crie um arquivo `.env` na raiz do projeto com o seguinte conteúdo, ajustando os valores conforme necessário:

```env
MYSQL_VERSION=5.7
CONTAINER_NAME_MYSQL=db_zabbix
HOSTNAME_MYSQL=db_zbxsrvbr
MYSQL_ROOT_PASSWORD=MYSQLROOTPASS
MYSQL_DATABASE=zabbix
MYSQL_USER=zabbix
MYSQL_PASSWORD=MYSQLUSERPASS
VOLUME_MYSQL_DATA=./zabbix/mysql
VOLUME_MYSQL_INITDB=./zabbix/initdb.d
ZABBIX_SERVER_IMAGE=zabbix/zabbix-server-mysql:ubuntu-6.4-latest
CONTAINER_NAME_ZABBIX_SERVER=server_zabbix
HOSTNAME_ZABBIX_SERVER=zabbixserver
DB_SERVER_HOST=db_zbxsrvbr
ZBX_ALLOWUNSUPPORTEDDBVERSIONS=1
VOLUME_ZABBIX_ALERTSCRIPTS=./zabbix/alertscripts
ZABBIX_WEB_IMAGE=zabbix/zabbix-web-nginx-mysql:alpine-6.4-latest
CONTAINER_NAME_ZABBIX_FRONTEND=frontend_zabbix
HOSTNAME_ZABBIX_WEB=web_zabbix-frontend
PHP_TZ=America/Sao_Paulo
VOLUME_NGINX_CONF=./nginx.conf
VOLUME_NGINX_CERTS=../PATH/TO/CERTS
ZABBIX_AGENT_IMAGE=zabbix/zabbix-agent2:alpine-6.4-latest
CONTAINER_NAME_ZABBIX_AGENT=agent_zabbix
HOSTNAME_ZABBIX_AGENT=zabbix-agent
ZBX_ACTIVE_ALLOW=false
VOLUME_ZABBIX_PLUGINS=./zabbix/plugins.d
VOLUME_ZABBIX_SCRIPTS=./zabbix/scripts
GRAFANA_IMAGE=grafana/grafana-enterprise
CONTAINER_NAME_GRAFANA=grafana
GRAFANA_USER=0
GF_SERVER_ROOT_URL=https://SEUDOMINIO.com/grafana
GF_SERVER_CERT_FILE=/ssl/cert.pem
GF_SERVER_CERT_KEY=/ssl/key.pem
GF_SERVER_PROTOCOL=https
GF_SERVER_HTTP_PORT=443
VOLUME_GRAFANA_DATA=./grafana/data
VOLUME_GRAFANA_CERTS=../PATH/TO/CERTS

```

## Iniciando os Serviços

Para iniciar todos os serviços definidos no Docker Compose, execute o seguinte comando no terminal:
```
docker-compose up -d
```

## Acesso aos Serviços

Zabbix Frontend: 

Frontend do Zabbix.
```
http://<SEU_DOMINIO>:80 ou https://<SEU_DOMINIO>:443
```
Grafana: 
```
http://<SEU_DOMINIO>:3000
```


## Configuração Pós-Instalação:


Siga as instruções de configuração específicas do Zabbix e Grafana para concluir a configuração dos serviços.
Configure dashboards no Grafana conforme necessário para visualizar os dados de monitoramento.


## Manutenção:

### Backup e Restauração:

MySQL: Faça backup do volume de dados MySQL regularmente.
Zabbix: Faça backup das configurações personalizadas e scripts.
Grafana: Faça backup dos dashboards e fontes de dados.

### Atualização:

Para atualizar para novas versões dos serviços, ajuste as imagens no arquivo docker-compose.yml e execute:
docker-compose down
docker-compose pull
docker-compose up -d

## Suporte:

Para suporte, consulte a documentação oficial dos serviços utilizados ou abra uma issue neste repositório.

Este README oferece uma visão geral básica para iniciar o projeto. Ajuste conforme necessário para atender aos requisitos específicos do seu ambiente.
