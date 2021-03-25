# Start with mutagen
mutagen project terminate && mutagen project start

# Download4
docker exec -it m2-php-fpm composer create-project -vvv --repository-url=https://repo.magento.com/ magento/project-community-edition .

# Install
docker exec -it m2-php-fpm php ./bin/magento setup:install --base-url=http://magento2.local/ \
    --db-host=db \
    --db-name=magento2 \
    --db-user=root \
    --db-password=1234qwer \
    --admin-firstname=Luiz \
    --admin-lastname=Tucillo \
    --admin-email=me@luiztucillo.com.br \
    --admin-user=admin \
    --admin-password=1234qwer \
    --elasticsearch-host=es01 \
    --language=pt_BR \
    --currency=BRL \
    --timezone=America/Sao_Paulo \
    --use-rewrites=1

# Test Elasticsearch
curl -X GET "localhost:9200/_cat/nodes?v=true&pretty"