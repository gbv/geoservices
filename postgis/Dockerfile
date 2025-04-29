FROM postgis/postgis:17-3.5

RUN apt-get update && apt-get install -y postgresql-17-ogr-fdw postgresql-server-dev-17 libcurl4-openssl-dev make g++ pgagent postgresql-17-cron

COPY ./pgsql-http /opt/pgsql-http
RUN cd /opt/pgsql-http && make && make install
