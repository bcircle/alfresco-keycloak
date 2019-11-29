## User

```bash
ldapmodify -h localhost -D "cn=admin,dc=example,dc=org" -w admin -p 10389 -a -f ldap/d.ldif
```

## Copy
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