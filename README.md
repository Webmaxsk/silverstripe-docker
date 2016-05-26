# silverstripe-docker-lamp
Silverstripe lamp docker setup based on https://github.com/4j5/silverstripe-lamp but without node/ruby part.

Stack built with:
- Debian Jessie - with backports repo
- MariaDB
- PHP5, PHPUnit, Composer, Phing
- SSPAK


## Project structure

       Project root
       /         \
    utils    	  public
      |         	    \
    remote.sspak.phar  	Silverstripe files


Add /utils folder to project root with remote.sspak.phar file for auto generating db and assets.


## Run

Run from "Project root" directory (port 3000, name "PROJECT") and visit http://localhost:3000 in browser
```bash
docker run -dP -p 3000:80 -v $(pwd):/var/www --name PROJECT webmaxsk/silverstripe-docker
```


If you have some big remote.sspak.phar, docker will create container, but is not ready yet. Check if is everything ready:
```bash
docker logs PROJECT
```

Manually load remote sspak (remote.sspak.phar)
```bash
docker exec -it PROJECT mysspak load remote
```


Manually save local sspak (will be stored in utils folder as local.sspak.phar)
```bash
docker exec -it PROJECT mysspak save local
```



Composer usage
```bash
docker exec -it PROJECT mycomposer parameter
```


Login to container and execute custom script
```bash
docker exec -it PROJECT bash
```

## Create custom version

Clone this repository to "Project root", customize and run command bellow. It will create image with name "sslamp". You can use your customized version when running new containers, just change "webmaxsk/silverstripe-docker" with "sslamp" in run command above.
```bash
docker build -t sslamp .
```


## Repos

- Docker: https://hub.docker.com/r/webmaxsk/silverstripe-docker/
- Github: https://github.com/Webmaxsk/silverstripe-docker/
