FROM postgis/postgis:15-3.3

RUN apt-get update && apt-get install -y postgresql-15-ogr-fdw postgresql-server-dev-15 libcurl4-openssl-dev make g++

COPY ./pgsql-http /opt/pgsql-http
RUN cd /opt/pgsql-http && make && make install
