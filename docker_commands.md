# Docker Commands

- `cat docker-compose.yml` : View docker-compose.yml.

## Run

- `docker-compose up` : Run docker-compose.
- `docker-compose ps` : List running containers.
- `docker-compose down` : Stop docker-compose.

## Build

- `docker-compose build` : Build docker-compose.

## Restart

- `docker-compose restart` : Restart docker-compose.

## Logs

- `docker-compose logs` : View docker-compose logs.
- `docker-compose logs -f` : Follow docker-compose logs.
- `docker-compose logs -t` : Tail docker-compose logs.
- `docker-compose logs -f -t` : Follow and tail docker-compose logs.

## Docker commands

## List

- `docker ps -all` : List all containers.
- `docker image ls` : List all images.
- `docker inspect <container_name>` : Inspect container.
- `docker logs <id>` : View container logs.
- `docker logs -f <id>` : Follow container logs.
- `docker info` : View docker info.
- `docker stats` : View docker stats.
- `docker inspect --format ='{{range .NetworkSettings.Networks}} {{.IPAddress}} {{end}}' id` : View container IP address.

## Run

- `docker container run --detach <container_name>` : Run container.

## Enter

- `docker exec -it <container_name> bash` : Enter to container.

## Stats

- `docker stats` : View docker stats.

## IP

- `docker inspect --format ='{{range .NetworkSettings.Networks}} {{.IPAddress}} {{end}}' id` : View container IP address.

## Build

- `docker build .` : Build docker image.
- `docker-compose up --build` : Build docker-compose.

## Run in background

- `docker-compose up -d` : Run docker-compose in background.
