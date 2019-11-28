## Alfresco and Keycloak Integration

- [Alfresco Identity Service](https://community.alfresco.com/people/gravitonian/blog/2018/07/17/getting-started-with-alfresco-identity-service-ea-keycloak)
- [Source](https://github.com/gravitonian/alfresco-dbp-keycloak-integration)
- http://localhost:8081/share
- http://localhost:8080/auth/admin/master/console
- http://localhost:8080/auth/realms/alfresco-dbp
- http://wk-MacBook.local:8080/auth

#### Global Properties

```bash
authentication.chain=identity-service1:identity-service,alfrescoNtlm1:alfrescoNtlm
identity-service.authentication.enabled=true
identity-service.enable-basic-auth=true
identity-service.authentication.defaultAdministratorUserNames=admin
identity-service.authentication.validation.failure.silent=false
identity-service.auth-server-url=http://wk-macbook.local:8080/auth
identity-service.realm=alfresco-dbp
identity-service.resource=alfresco-client
identity-service.public-client=true
identity-service.ssl-required=non
```

#### Restart Content Service

```bash
docker-compose stop content
docker-compose rm -f content
docker-compose up -d --no-deps content
```

#### Test Authentication

```bash
curl http://localhost:8080/auth/realms/alfresco-dbp

curl -d 'client_id=alfresco-client' \
    -d 'username=wk@gmail.com' \
    -d 'password=1234' \
    -d 'grant_type=password' \
    'http://localhost:8080/auth/realms/alfresco-dbp/protocol/openid-connect/token' | python -m json.tool

curl -d 'client_id=alfresco-client' \
    -d 'username=admin@gmail.com' \
    -d 'password=1234' \
    -d 'grant_type=password' \
    'http://wk-macbook.local:8080/auth/realms/alfresco-dbp/protocol/openid-connect/token' | python -m json.tool

curl -d 'client_id=alfresco-client' \
    -d 'username=wk' \
    -d 'password=1234' \
    -d 'grant_type=password' \
    'http://wk-macbook.local:8080/auth/realms/alfresco-dbp/protocol/openid-connect/token' | python -m json.tool
```

```bash
curl http://wk-macbook.local:8082/alfresco/api/-default-/public/alfresco/versions/1/nodes/-root-/children \
    -H "Authorization: bearer <TOKEN>"  | python -m json.tool
```

## Resource

- https://blog.johanet.fr/single-sign-on-with-alfresco-share-and-keycloak
- https://hub.alfresco.com/t5/alfresco-platform-services-blog/getting-started-with-alfresco-identity-service-ea-keycloak/ba-p/288261
- https://www.mai1015.com/development/2019/05/05/docker-keycloak-proxy-behind-nginx
- https://hub.alfresco.com/t5/application-development/adf-2-4-0-release-note/ba-p/293335