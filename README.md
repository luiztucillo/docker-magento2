# INSTRUCTIONS


## INITIAL CONFIG
- Define `server_name` in `images/nginx/conf/conf.d/default.conf`
- Define username in `images/php/php-fpm;conf:11,12`, `images/php/Dockerfile:6,7,9,27`  and `images/nginx/conf/nginx.conf`


## DOWNLOAD MAGENTO
- If the composer is >= 2.0, runs `sudo composer self-update --1`
- Runs inside continer
  - `composer create-project -vvv --repository-url=https://repo.magento.com/ magento/project-community-edition /var/www/html/tmp && mv tmp/* ./ && mv tmp/.* ./ &&        rm -rf /var/www/html/tmp`

## INSTALL MAGENTO
Set the vars below and run:
```
bin/magento setup:install \
    --base-url=http://localhost/ \
    --db-host=mysql \
    --db-name=dev_magento2 \
    --db-user=root \
    --db-password=1234qwer \
    --admin-firstname=Admin \
    --admin-lastname=ADmin \
    --admin-email=admin@admin.com \
    --admin-user=admin \
    --admin-password=1234qwer \
    --language=pt_BR \
    --currency=BRL \
    --timezone=America/Sao_Paulo \
    --use-rewrites=1 \
    --elasticsearch-port=9200 \
    --elasticsearch-host=elk \
    --search-engine=elasticsearch7
```

### CONFIGURE SESSION
```
bin/magento setup:config:set \
    --session-save=redis \
    --session-save-redis-host=redis \
    --session-save-redis-port=6379 \
    --session-save-redis-log-level=4 \
    --session-save-redis-db=2
```

### CONFIGURE CACHE
```
bin/magento setup:config:set \
    --page-cache=redis \
    --page-cache-redis-port=6379 \
    --page-cache-redis-server=redis \
    --page-cache-redis-db=1
```

## Configure XDebug
As *PHP-FPM* uses *PORT __9000__*, xdebug was set to use *PORT __9001__* so you need to set your *IDE* port of *XDEBUG* to *__9001__*

## Access Mysql from HOST AND Application
Add to the */etc/hosts* file: __*127.0.0.1 mysql.localhost*__

## Magento 2 instal
- Enter php container. DON'T USE ROOT
```bash
docker container exec -it m2_php bash
```
- Download Magento2 from composer
```bash
cd /var/www/html && composer create-project --repository-url=https://repo.magento.com/ magento/project-community-edition
```
- Move files to root (Composer prevent create project inside non empty folder. So we download inside another folder and then move then back)
```bash
cp -r project-community-edition/* ./ && rm -rf project-community-edition
```
- Install Magento2
```bash
php ./bin/magento setup:install --base-url=http://magento2.local/ \
--db-host=mysql --db-name=dev_magento2 --db-user=root --db-password=1234qwer \
--admin-firstname=Luiz --admin-lastname=Tucillo --admin-email=me@luiztucillo.com.br \
--admin-user=suporte --admin-password=1234qwer --language=pt_BR \
--currency=BRL --timezone=America/Sao_Paulo --use-rewrites=1
```
