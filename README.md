# NFIS Geoservices

## Installation

1. Download the geostyler geoserver plugin JAR file [here](https://nexus.terrestris.de/#browse/browse:geoserver-extras:org%2Fgeoserver%2Fcommunity%2Fgs-geostyler%2F1.2.2%2Fgs-geostyler-1.2.2-2.22.2.jar) and save it in the directory "geoserver-plugins".

2. Open the files "nginx/nginx.conf" and "geoserver-config/web.xml" and replace [SERVERNAME] with your server domain name.

3. Open the file "docker-compose.yml" and replace each occurrence of [EMAIL] and [PASSWORD] with the respective value.

3. Run:
```
docker compose up -d
```

## Services

### PGAdmin
Available in browser via "[SERVERNAME]/pgadmin"
### Geoserver
Available in browser via "[SERVERNAME]/geoserver"
### PostGIS
Available via "[SERVERNAME]:5432"
