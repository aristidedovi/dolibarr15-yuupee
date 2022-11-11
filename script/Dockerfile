#Create MySQL Image for JSP Tutorial Application
FROM mysql

ENV MYSQL_ROOT_PASSWORD aristide
ENV MYSQL_DATABASE dolibarr
ENV MYSQL_USER aristide
ENV MYSQL_PASSWORD aristide

ADD ./data/script.sql /docker-entrypoint-initdb.d/script.sql
#RUN mysql dolibarr -u aristide -paristide < docker-entrypoint-initdb.d/script.sql
