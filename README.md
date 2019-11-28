## Keycloak

```bash
docker login reg.bcecm.com

docker-compsoe up

docker-compose stop proxy
docker-compose stop identity-service
docker-compose stop alfresco

docker-compose up -d content-app
docker-compose up -d proxy
docker-compose up -d ldap
docker-compose up -d identity-service
docker-compose up -d --no-deps  alfresco
```

## Development

```bash
docker run \
    --rm \
    --entrypoint cat alfresco/acs-community-ngnix:1.0.0 /etc/nginx/nginx.conf > \
    nginx/nginx.conf

docker run \
    --rm \
    --entrypoint cat reg.bcecm.com/beflex-content-management/beflex-content-app:1.7.15.20190926.5 /usr/share/nginx/html/app.config.json > \
    content-app/app.config.json

docker run \
    --rm \
    --entrypoint cat alfresco/alfresco-content-repository-community:6.2.0-ga /usr/local/tomcat/shared/classes/alfresco-global.properties > \
    acs/default.properites

docker run \
    --rm \
    --entrypoint cat alfresco/alfresco-content-repository-community:6.2.0-ga /usr/local/tomcat/shared/classes/alfresco-global.properties

docker run \
    --rm \
    --entrypoint ls alfresco/alfresco-content-repository-community:6.2.0-ga /usr/local/tomcat/shared/classes
```

- http://localhost:8080
- http://localhost:8080/alfresco
- http://localhost:8080/share
- http://localhost:8080/auth

## Tests

- http://localhost:8080/auth/realms/alfresco-dbp/protocol/openid-connect/auth?response_type=code&client_id=alfresco-client&redirect_uri=https://google.com


```bash
curl -d 'client_id=alfresco-client' \
    -d 'username=admin' \
    -d 'password=1234' \
    -d 'grant_type=password' 'http://localhost:8080/auth/realms/alfresco-dbp/protocol/openid-connect/token' | python -m json.tool


## Resource

- https://hub.alfresco.com/t5/alfresco-content-services-forum/how-to-synchronize-alfresco-users-with-keycloak-share-not-aps/m-p/89993