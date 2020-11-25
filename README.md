# INSTRUCTIONS


## INITIAL CONFIG
- Define `server_name` in `images/nginx/conf/conf.d/default.conf`
- Define username in `.env` and `images/php/php-fpm;conf:11,12`





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
