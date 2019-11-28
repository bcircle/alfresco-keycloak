## Keycloak

```bash
docker login reg.bcecm.com

docker-compsoe up
docker-compose up -d content-app

docker-compose stop proxy
docker-compose up -d proxy
```

## Development

```bash
docker run --rm --entrypoint cat alfresco/acs-community-ngnix:1.0.0 /etc/nginx/nginx.conf > nginx/nginx.conf
```

- http://localhost:8080/alfresco
- http://localhost:8080/share