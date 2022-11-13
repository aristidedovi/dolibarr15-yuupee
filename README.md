# Using Docker Compose with Datadog

Datadog offers native Docker container monitoring, either by running the Agent
on the host or running in a sidecar container. Which is the best way to run it?
It ultimately depends on the tooling you have in place to manage the Agent's
configuration. If you want to go Docker all the way, you can run the Agent as
a sidecar and control its configuration with custom `Dockerfiles`.

Let's see what it looks like.

# Starting off from the Compose example

To build a meaningful setup, we start from the [example](https://docs.docker.com/compose/#overview)
that Docker put together to illustrate Compose. A simple python web application that
connects to Redis to store the number of hits.

Here is the `docker-compose.yml` that powers the whole setup.

```yaml
version: '3.8'
services:
  php-apache-environment:
    container_name: php-apache
    build:
        context: ./dolibarr-yuupee
        dockerfile: Dockerfile
    depends_on:
        - db
    volumes:
      - ./dolibarr-yuupee:/var/www/html/
    ports:
      - 8000:80
  db:
    container_name: db
    build:
        context: ./script
        dockerfile: Dockerfile
    restart: always
    volumes:
        - ./script/mysql:/var/lib/mysql
    ports:
        - "9906:3306"
  phpmyadmin:
    image: phpmyadmin/phpmyadmin
    ports:
        - '8080:80'
    restart: always
    environment:
        PMA_HOST: db
    depends_on:
        - db
```

# All in one

How to test this?

1. [Install Docker Compose](https://docs.docker.com/compose/install/)
1. Clone this repository
1. Run all containers with `docker-compose up`
1. Verify in Datadog that your container picks up the docker

# Super admin credential
Identifiant = superadmin
Mot de passe = tSAKcyk9JHO9