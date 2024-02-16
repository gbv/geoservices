FROM postgis/postgis:16-3.4

RUN apt-get update && apt-get install -y postgresql-16-ogr-fdw postgresql-server-dev-16 libcurl4-openssl-dev make g++

COPY ./pgsql-http /opt/pgsql-http
RUN cd /opt/pgsql-http && make && make install
