[getcomposer]: https://getcomposer.org/
[uninstall-mods]: https://getcomposer.org/doc/03-cli.md#remove

## Sobre o DevilBox

https://github.com/cytopia/devilbox

## Instalando o DevilBox

    cd ~/dados/dockers/
    git clone https://github.com/cytopia/devilbox
    cd devilbox
    cp env-example .env

## Configurando o DevilBox

### Devido a necessidade do uso do link simbólico.

Edite o arquivo docker-compose.yml

Adicione o seguinte registro

    # Mount volumes related to ln -s htdocs
    - /home/marcelo/dados/:/home/marcelo/dados/

Nas hierarquias php: / volumes e httpd: / volumes

### Editando a configuração do DevilBox

Edite o arquivo .env

    DOCKER_LOGS=1
    PHP_SERVER=7.0
    HTTPD_SERVER=apache-2.4
    HOST_PATH_HTTPD_DATADIR=/home/marcelo/dados/mount/www
    HOST_PATH_MYSQL_DATADIR=/home/marcelo/dados/mount/mysql
    PHP_MODULES_ENABLE=ioncube

## Iniciando o DevilBox

    cd ~/dados/dockers/devilbox

    docker-compose up

## Monitoramento de imagens e processos

    docker --version && docker images && docker images ps && docker ps

## Acessar o DevilBox

http://localhost/

## Paralisar o DevilBox

Pressione control + C

## Para uso após a reinicialização da máquina

    cd ~/dados/dockers/devilbox

    docker-compose down --remove-orphans

    cd ~/dados/dockers/devilbox

    docker-compose up

Ao reiniciar a máquina é carregado o servidor apache mas não o banco de dados devendo executar o comando acima.



cat > phpinfo.php <<- _EOF_
<?php phpinfo(); ?>
_EOF_

cat > composer.json <<- _EOF_
{
   "minimum-stability": "dev",
   "prefer-stable": true,
   "license": [
       "proprietary"
   ],
   "repositories":[
       {
           "type":"composer",
           "url":"https://packages.firegento.com"
       }
   ],
   "extra":{
       "magento-root-dir":"magento",
       "magento-deploystrategy": "copy",
       "magento-force": true
   },
   "require": {
       "magento-hackathon/magento-composer-installer": "~3.0",
       "aydin-hassan/magento-core-composer-installer": "~1.2",
       "firegento/magento": "~1.9.3.1"
   }
}
_EOF_

composer diagnose
