# NFIS Geoservices

## Installation

1. Download the geostyler geoserver plugin JAR file [here](https://nexus.terrestris.de/#browse/browse:geoserver-extras:org%2Fgeoserver%2Fcommunity%2Fgs-geostyler%2F1.2.2%2Fgs-geostyler-1.2.2-2.22.2.jar) and save it in the directory "geoserver-plugins".

2. Open the files "nginx/nginx.conf" and "geoserver-config/web.xml" and replace [SERVERNAME] with your server domain name.

3. Open the file "docker-compose.yml" and replace each occurrence of [EMAIL] and [PASSWORD] with the respective value.

4. Open the file "pgagent/pgpass" and replace [DATABASE_NAME] with the name of the database and [PASSWORD] with the password of the postgres database user as defined in docker-compose.yml.

5. Run:
```
docker compose up -d
```

## Services

### pgAdmin
Available in browser via "[SERVERNAME]/pgadmin"
### Geoserver
Available in browser via "[SERVERNAME]/geoserver"
### PostGIS
Available via "[SERVERNAME]:5432"


## Configure database backups

1. Open pgAdmin.
2. Create pgAgent extension for "postgres" database and the databases you want to backup:
    * Right click "Extensions"
	* Open Query tool
	* Type in "CREATE EXTENSION pgagent;"
	* Click "Execute/refresh" (play button)
3. Open "pgAgent Jobs" and create a new "batch" job with the following code (replace DATABASE_NAME with the name of the database to backup):

```
pg_dump --username=postgres --dbname=[DATABASE_NAME] --file=/postgis-backups/backup-`date +%Y-%m-%d_%H-%M`.pgdump --verbose -Fc
		cd /postgis-backups
		find . ! -name 'backup-????-??-01*' -mtime +7 -exec rm {} \;
```
4. Make sure the file pgagent/pgpass contains an entry for each database you want to backup.
