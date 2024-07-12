## keycloak

## To export realm and users to json

```bash
cd /opt/keycloak/bin
./kc.sh export --users realm --realm myrealm --dir /tmp/keycloak-export
```
The realm and users will be exported to /tmp/keycloak-export/myrealm-export.json

## To import realm and users from json

Note: For the Keycloak containers, the import directory is /opt/keycloak/data/import

```bash
cd /opt/keycloak/bin
./kc.sh import --file /tmp/realm-export.json
```

or to import realms when the server is starting by using the --import-realm option.
When you set the --import-realm option, the server is going to try to import any realm configuration file from the data/import directory.
Only regular files using the .json extension are read from this directory, sub-directories are ignored.

```bash
bin/kc.[sh|bat] start --import-realm
```

## If keycloak is hosted using docker

## Exporting

```bash
docker ps
docker exec -it <container_id> /bin/bash
```

Once Exported

```bash
docker cp <container_id>:/tmp/keycloak-export /path/on/your/vm
```

## Importing

```bash
docker cp /home/user/keycloak-export/realm-export.json <container_id>:/tmp/realm-export.json
```

once copied add the following to docker-compose

```bash
KEYCLOAK_IMPORT: /tmp/.json -Dkeycloak.profile.feature.upload_scripts=enabled
```

Once successfully copied

```bash
docker-compose up -d
```
