# Docker + MariaDB + PhpMyAdmin

## Links

http://127.0.0.1:81/ - PhpMyAdmin (`PHPMYADMIN_80` in `.env` config)

<br />

## Installation

1. Download folder.

2. Create the file `./.docker/.env` using `./.docker/.env.example` as template.<br />
    For multiple dockers you need change every time `COMPOSE_PROJECT_NAME` and `port` variables.

3. Go inside folder `./docker` and run `docker-compose up -d --build` to start containers.