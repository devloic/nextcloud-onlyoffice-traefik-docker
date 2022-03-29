# nextcloud-onlyoffice-traefik-docker
A Docker stack for Nextcloud with Onlyoffice behind Traefik, with https !


Change .env variable.

MOVED TO DOCKER-COMPOSE.YML : create frontend and database network

```
DONT RUN# docker network create --driver=overlay frontend
DONT RUN# docker network create --driver=overlay database
```

Start Traefik :
```
docker-compose -f docker-compose-traefik.yml up -d
```

Start Nextcloud Stack
```
docker-compose up -d
```


Configure Nextcloud.
Go inside the container :
```
docker exec -u www-data -ti <nextcloud app container> bash
```

allow to set onlyoffice as local container. Within the nextcloud container :
```
php occ --no-warnings config:system:set allow_local_remote_servers --value=true
```

MOVED TO .ENV AND DOCKER-COMPOSE.YML : add hostame container and domain to trusted domain :
```
DONT RUN# php occ --no-warnings config:system:set trusted_domains 1 --value="onlyoffice"
DONT RUN# php occ --no-warnings config:system:set trusted_domains 2 --value="nextcloud"
DONT RUN# php occ --no-warnings config:system:set trusted_domains 3 --value="<YOUR NEXTCLOUD_DOMAIN>"
DONT RUN# php occ --no-warnings config:system:set trusted_domains 4 --value="<YOUR ONLYOFFICE DOMAIN>"
```

go to your nextlcoud instance, install it, go to app and add Onlyoffice from the app store.
Configure it

```
php occ --no-warnings config:system:set onlyoffice DocumentServerUrl --value="http://<ONLYOFFICE.DOMAIN>"
php occ --no-warnings config:system:set onlyoffice DocumentServerInternalUrl --value="http://onlyoffice/"
php occ --no-warnings config:system:set onlyoffice StorageUrl --value="http://nextcloud/"
php occ --no-warnings config:system:get onlyoffice
php occ onlyoffice:documentserver --check
```
