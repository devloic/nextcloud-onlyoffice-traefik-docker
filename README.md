# nextcloud-onlyoffice-traefik-docker
A Docker stack for Nextcloud with redis with Onlyoffice behind Traefik (2.6.2), with https !


Change .env variable.

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
docker exec -u www-data -ti nextcloud_app bash
```

allow to set onlyoffice as local container. Within the nextcloud container :

```
php occ --no-warnings config:system:set allow_local_remote_servers --value=true
```

go to your nextlcoud instance, install it, go to app and add Onlyoffice from the app store.
Configure it

```
php occ --no-warnings config:system:set onlyoffice DocumentServerUrl --value="https://<ONLYOFFICE.DOMAIN>"
php occ --no-warnings config:system:set onlyoffice DocumentServerInternalUrl --value="https://<ONLYOFFICE.DOMAIN>/"
php occ --no-warnings config:system:set onlyoffice StorageUrl --value="https://<NEXTCLOUD.DOMAIN>/"
php occ --no-warnings config:system:get onlyoffice
php occ onlyoffice:documentserver --check
```
