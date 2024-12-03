FROM ubuntu:24.04

RUN apt-get update
RUN apt-get install -y dirmngr ca-certificates software-properties-common apt-transport-https lsb-release curl

RUN sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'
RUN curl -fsSL https://www.postgresql.org/media/keys/ACCC4CF8.asc | gpg --dearmor -o /etc/apt/trusted.gpg.d/postgresql.gpg

RUN apt-get update
RUN apt-get install -y postgresql-client-17

ENV TIMEZONE_VALUE=Europe/Berlin
RUN ln -snf /usr/share/zoneinfo/$TIMEZONE_VALUE /etc/localtime && echo $TIMEZONE_VALUE > /etc/timezone
RUN apt-get update
RUN apt-get install -y pgagent

CMD ["pgagent", "-f", "host=postgis", "port=5432", "dbname=postgres", "user=postgres", "-l", "1"]
