## keycloak

## To export realm and users to json

```bash
cd /opt/keycloak/bin
./kc.sh export --users realm --realm myrealm --dir /tmp/keycloak-export
```
The realm and users will be exported to /tmp/keycloak-export/myrealm-export.json

## To import realm and users from json

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

Note: For the Keycloak containers, the import directory is /opt/keycloak/data/import

## If keycloak is hosted using docker

## Exporting

```bash
docker ps
docker exec -it <container_id> /bin/bash
```

Once Exported copy to vm using

```bash
docker cp <container_id>:/tmp/keycloak-export /path/on/your/vm
```

## Importing (vm to container)

```bash
docker cp /home/user/keycloak-export <container_id>:/tmp
```

or copy to default import directory

```bash
docker cp /home/user/keycloak-export <container_id>:/opt/keycloak/data/import

```

once copied add the following to docker-compose

```bash
KEYCLOAK_IMPORT: /tmp/.json -Dkeycloak.profile.feature.upload_scripts=enabled
```

Once successfully copied

```bash
docker-compose up -d
```
