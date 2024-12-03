# Geoservices

Configuration files for running geoservices (Geoserver, PostGIS, pgAdmin, pgAgent) for NFIS and archaeoDox.

## Installation

1. Download submodule pgsql-http:
```
git submodule update --init
```

2. Copy desired Geoserver plugin files to the directory "geoserver-plugins".

3. Copy the following files:
	* "docker-compose.template.yml" to "docker-compose.yml"
	* "nginx/nginx.template.conf" to "nginx/nginx.conf"
	* "geoserver-config/web.template.xml" to "geoserver-config/web.xml"
	* "pgagent/pgpass.template" to "pgagent/pgpass"

4. Open the files "nginx/nginx.conf" and "geoserver-config/web.xml" and replace [SERVERNAME] with your server domain name.

5. Open the file "docker-compose.yml" and replace each occurrence of [EMAIL] and [PASSWORD] with the respective value.

6. Open the file "pgagent/pgpass" and replace [DATABASE_NAME] with the name of the database and [PASSWORD] with the password of the postgres database user as defined in docker-compose.yml.

7. Create nginx logfile:
```
touch nginx/error_log.log
```

8. Run:
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

When changing the pgpass file at a later time, make sure to restart the pgagent container afterwards.

## Restore backup
```
pg_restore -d [DATABASE_NAME] -Fc -U [USER_NAME] [FILE_PATH]
```
