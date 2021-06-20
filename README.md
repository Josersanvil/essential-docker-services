# Essential development services

Docker compose files to start important services for development in the host's network.

## Services

The file `docker-compose.yml` can be used to spin-up containers for the following services:

name | description | docker image | default endpoint
---- |------------ | ------------ | ----------------
**postgres** | PostgreSQL server (SQL Database). | [link](https://hub.docker.com/_/postgres) | `localhost:5432`
**pgadmin** | Web based admin platform for PostgreSQL. | [link](https://hub.docker.com/r/dpage/pgadmin4/) | `localhost:64503`
**mongodb** | MongoDB server (NoSQL JSON Database). | [link](https://hub.docker.com/_/mongo) | `localhost:27017`
**mongo-express** |Web-based MongoDB admin interface. | [link](https://hub.docker.com/_/mongo-express) | `localhost:8081`
**redis** | Redis server, an in-memory key–value database, cache and message broker. | [link](https://hub.docker.com/_/mongo-express) | `localhost:6379`

> The `latest` tag of the docker images are used.

`mongo_docker-compose.yml` spins-up containers for **mongodb**, **mongo-express** and **redis**.

## Setup

Requires Docker Engine 19.03.0+

Install Docker: https://docs.docker.com/engine/install/

### .env configuration file

Edit the `.env` file with the environment variables to configure the containers.

It is recommended to set the following environment variables in the file:

Name | Description | Default value | Required
---- |------------ | ------------- | --------
**POSTGRES_DB** | Name of a postgres database to create. | `postgres` | &cross;
**POSTGRES_USER** | Username to connect to the postgres server. | `postgres` | &cross;
**POSTGRES_PASSWORD** | Password to connect to the postgres server. | | &check;
**POSTGRES_FWD_PORT** | Port to forward for the postgres server. | `5432` | &cross;
**PGADMIN_DEFAULT_EMAIL** | Email to use to connect to the pgadmin web app. | | &check;
**PGADMIN_DEFAULT_PASSWORD** | Password to use to connect to the pgadmin web app. | | &check;
**PGADMIN_FWD_PORT** | Port to forward for the pgadmin web service (Default '80'). | `64503` | &cross;
**MONGODB_USERNAME** | Username to use to connect to the mongodb server. | `mongo` | &cross;
**MONGODB_PASSWORD** | Password to use to connect to the mongodb server. | | &check;
**MONGODB_FWD_PORT** | Port to forward for the mongodb server | `27017` | &cross;
**REDIS_FWD_PORT** | Port to forward for the redis server | `6379` | &cross;
**MONGOEXPRESS_ADMIN_USERNAME** | Username to use to connect to the mongo-express web app | `admin` | &cross;
**MONGOEXPRESS_ADMIN_PASSWORD** | Password to use to connect to the mongo-express web app | | &check;
**MONGOEXPRESS_FWD_PORT** | Port to forward for the mongo-express web service | `8081` | &cross;
**DOCKER_RESTART_POLICY** | Restart Policy for the docker container | `unless-stopped` | &cross;

## Run

Start the containers by running:
```
docker-compose up -d --build
```

Get the logs using: `docker-compose logs -f`

Stop the containers using `docker-compose down`

Or if you want to delete all data associated with the containers use `docker-compose down -v`

To specify the docker-compose file to use just use the `-f` argument like:
```
docker-compose -f mongo_docker-compose.yml up -d --build
```