# NFIS Geoservices

## Installation

1. Download the geostyler geoserver plugin JAR file [here](https://github.com/geostyler/geostyler-geoserver-plugin/packages/1469140) and save it in the directory "geoserver-plugins".

2. Open the file "nginx/nginx.conf" and replace [SERVERNAME] with your server domain name.

3. Open the file "docker-compose.yml" and replace each occurrence of [USERNAME], [EMAIL] and [PASSWORD] with the respective value.

3. Run:
```
docker compose up -d
```
