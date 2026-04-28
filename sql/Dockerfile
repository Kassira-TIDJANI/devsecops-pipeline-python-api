FROM mysql:8.0

ENV MYSQL_ROOT_PASSWORD=root
ENV MYSQL_DATABASE=beer
ENV MYSQL_USER=user1
ENV MYSQL_PASSWORD=user1_password

COPY ./beer.sql /docker-entrypoint-initdb.d/

EXPOSE 3306