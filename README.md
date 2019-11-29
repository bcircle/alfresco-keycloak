## Keycloak

```bash
docker login reg.bcecm.com
docker-compsoe up
```

## Development

- http://localhost/
- http://localhost/alfresco
- http://localhost/share
- http://localhost:8080/auth

## Tests

- http://localhost:8080/auth/realms/alfresco-dbp/protocol/openid-connect/auth?response_type=code&client_id=alfresco-client&redirect_uri=https://google.com

```bash
curl -d 'client_id=alfresco-client' \
    -d 'username=admin' \
    -d 'password=1234' \
    -d 'grant_type=password' 'http://localhost:8080/auth/realms/alfresco-dbp/protocol/openid-connect/token' | python -m json.tool

brew cask install apache-directory-studio
```

## Resource

- https://hub.alfresco.com/t5/alfresco-content-services-forum/how-to-synchronize-alfresco-users-with-keycloak-share-not-aps/m-p/89993
- https://henningwaack.wordpress.com/2018/05/24/keycloak-snippets-keycloak-quickstarts-struggles/