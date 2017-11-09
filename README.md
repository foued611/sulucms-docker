SULU CMS Docker (optimized for local dev env)
=============================================


```

#### build docker images
```bash
docker-compose build
```

#### use docker container with docker sync (performance optimization for mac & Windows)
Documentation: https://github.com/EugenMayer/docker-sync/wiki
```bash
#install docker sync
#No matter if its OSX/Linux/Windows

gem install docker-sync

#Start Docker containers & sync 
docker-sync-stack start

```

#### use docker container without docker sync
```bash
docker-compose build 
docker-compose -f docker-compose.yml -f docker-no-sync.yml up

```

#### connect to php fpm container 
```bash
# connect to php fpm container were the document root is placed 
docker exec -it sulucms_php-fpm bash

# install dependency & initialise sulu Database
composer install
bin/adminconsole sulu:build dev
```

### configured host 
 
 https://sulu.dev

- (only initial or after changes) docker-compose build - __build your images__

- docker-compose up -d - __run your services__

- docker-compose stop - __stop your services__

- docker exec -it container-name /bin/bash - __connect to service__

- (warning) docker stop $(docker ps -a -q) - __stop ALL of Docker containers__

- (warning) docker rm -f $(docker ps -a -q) - __remove ALL of Docker containers__

- (warning) docker rmi -f $(docker images -a -q) - __remove ALL of Docker images__
