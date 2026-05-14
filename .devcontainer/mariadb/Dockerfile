FROM mariadb:latest

# Instala wget y unzip para descargar la base de datos Sakila
RUN apt-get update && apt-get install -y wget unzip && \
    wget https://downloads.mysql.com/docs/sakila-db.zip -O /tmp/sakila.zip && \
    unzip /tmp/sakila.zip -d /tmp/ && \
    # Mueve los archivos SQL a la carpeta de inicialización de MariaDB
    mv /tmp/sakila-db/sakila-schema.sql /docker-entrypoint-initdb.d/01-sakila-schema.sql && \
    mv /tmp/sakila-db/sakila-data.sql /docker-entrypoint-initdb.d/02-sakila-data.sql && \
    # Limpieza
    rm -rf /tmp/sakila.zip /tmp/sakila-db && \
    apt-get purge -y wget unzip && apt-get autoremove -y && rm -rf /var/lib/apt/lists/*

ENV MARIADB_ROOT_PASSWORD=root
ENV MARIADB_DATABASE=sakila
