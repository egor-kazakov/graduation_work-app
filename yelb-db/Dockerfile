FROM postgres:10.0

WORKDIR /

COPY init-yelb-db.sh /docker-entrypoint-initdb.d/init-yelb-db.sh

ENV POSTGRES_USER=dbuser
ENV POSTGRES_PASSWORD=password
