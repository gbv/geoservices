FROM ubuntu:22.04

RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install -y dirmngr ca-certificates software-properties-common apt-transport-https lsb-release curl

RUN curl -fSsL https://www.postgresql.org/media/keys/ACCC4CF8.asc | gpg --dearmor | tee /usr/share/keyrings/postgresql.gpg > /dev/null

RUN echo deb [arch=amd64,arm64,ppc64el signed-by=/usr/share/keyrings/postgresql.gpg] http://apt.postgresql.org/pub/repos/apt/ $(lsb_release -cs)-pgdg main | tee /etc/apt/sources.list.d/postgresql.list

RUN apt-get update
RUN apt-get install -y postgresql-client-16

ENV TIMEZONE_VALUE=Europe/Berlin
RUN ln -snf /usr/share/zoneinfo/$TIMEZONE_VALUE /etc/localtime && echo $TIMEZONE_VALUE > /etc/timezone
RUN apt-get update
RUN apt-get install -y pgagent

CMD ["pgagent", "-f", "host=postgis", "port=5432", "dbname=postgres", "user=postgres", "-l", "1"]
