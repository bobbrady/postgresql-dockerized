# PostgreSQL Dockerized

A simple PostgreSQL docker container with usage instructions, utilizing the lastest version of PostgreSQL.

## Usage

The docker container is built and run via the docker-compose.yml script in this project. The following are the defaults:

- User: test
- Password: test
- Database: test

The above settings can also be set by having a .env properties file configured with the same `docker-compose.yml` variables.

The init.d directory contains scripts that will be run in alphabetical order at server start-up time. You can add/remove/modify scripts here. There is a starter script `10-test-ddl.sql` with DDL to create a table on start-up.

First, build the image and run in background detached mode:

```
# builds the image if doesn't exist, binds port 5432 on localhost to container db
docker-compose up -d
```

Next, obtain an interactive bash shell to the running container:

```
docker exec -it postgres bash

# Use the psql CLI to issue SQL statements
psql -U root -d test_db

```

## Clean-up and Reset

The PostgreSQL data directory is persisted across container starts. You can delete it as follows:

```
docker volume rm -f pgdata
```

To start with a clean docker envrionment, do this:

```
docker rm -f $(docker ps -a -q)
docker system prune -a --volumes
```
