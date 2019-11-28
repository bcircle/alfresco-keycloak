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

eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICJ6QjhwejhVZ2dqVDBUUFFJdjFTUFZOMnVFNHZrTjhLN0thTVRkU1VWOTFJIn0.eyJqdGkiOiIxOWM0YzUwOC00MzdjLTRiYTMtYmM5Ny05ZGNlYjA1YWM5ZmUiLCJleHAiOjE1NzQ5NDE1OTUsIm5iZiI6MCwiaWF0IjoxNTc0OTM5Nzk1LCJpc3MiOiJodHRwOi8vbG9jYWxob3N0OjgwODAvYXV0aC9yZWFsbXMvYWxmcmVzY28tZGJwIiwiYXVkIjoiYWxmcmVzY28tY2xpZW50Iiwic3ViIjoiMzJjYjZkNjYtOWQyZi00ODMyLTk2ZDAtZDZkZDNlMTBmYzJjIiwidHlwIjoiUmVmcmVzaCIsImF6cCI6ImFsZnJlc2NvLWNsaWVudCIsImF1dGhfdGltZSI6MCwic2Vzc2lvbl9zdGF0ZSI6IjllNjgwNTYyLTkxNWItNGY4ZS1hMTk0LWQwYjRiZTJmY2FkNCIsInJlYWxtX2FjY2VzcyI6eyJyb2xlcyI6WyJ1bWFfYXV0aG9yaXphdGlvbiJdfSwicmVzb3VyY2VfYWNjZXNzIjp7ImFjY291bnQiOnsicm9sZXMiOlsibWFuYWdlLWFjY291bnQiLCJtYW5hZ2UtYWNjb3VudC1saW5rcyIsInZpZXctcHJvZmlsZSJdfX19.cAaQ2jhizThz9DDFJALgNhzaubusqMmDZEFvpBAc10F3PclYQgT4R5RPZLUpSryBoUWYj3rUgAQXwERusknplDOyBkdOOs-B2h_1mKHWXNN81lyJV31YMcZNC2YbNI_Qiypdfu9VRtXURoLDARRfJ0L-cRG8zJCy0PtQBzVOMZVbiTiLgFUqBsAD9hr4L6tpOUfl2bVFcuq3xvE7pz9BCwbPEOkGbcUuixqpAZ96PeBKE-8hqrSwymBHV18SVrx3izlnlWS-e9Lt5PRony5w2ALcbQnDjpMwdfdttqGqhH28zUapYtja8q023Rx6mYN-hNvfz-Ii87hBLchYK6uAnQ