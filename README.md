# Initial docker

### Windows commands

```Create network
docker network create network

```Build images
docker-compose build

```Running containers
docker-compose up -d

```Stop containers
docker-compose stop

### Linux or MAC Scripts
*Using **Makefile***: https://makefiletutorial.com/

Installs composer dependencies

```shell
make prepare
```

Build the containers

```shell
make build
```

Start the containers

```shell
make run
```

Stop the containers

```shell
make stop
```

Restart the containers

```shell
make restart
```

### Steps to follow

Init the bash shell into the **Backend container**

```shell
make ssh-be
```

Update packages

```shell
composer update
```

Install packages

```shell
composer install
```

