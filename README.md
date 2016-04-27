# silverstripe-docker-lamp
Silverstripe lamp docker setup based on https://github.com/4j5/silverstripe-lamp but without node/ruby part.

## Build image

Stack built with:
- Debian Jessie - with backports repo
- MariaDB
- PHP5, PHPUnit, Composer, Phing
- SSPAK

Clone this repository to Project root and run command bellow. It will create image with name "sslamp".
```bash
docker build -t sslamp .
```

## Project structure


       Project root
       /      	\
    utils    	  public
      |         	\
    remote.sspak.phar  	Silverstripe files


Add /utils folder to project root with remote.sspak.phar file for auto generating db and assets.

## Run

running from Project root directory and set to port 3000

Assign name "project" to container and visit http://localhost:3000
```bash
docker run -dP -p 3000:80 -v $(pwd):/var/www --name project sslamp
```

If you have some big remote.sspak.phar, docker will create container, but is not ready yet. Check if is everything ready:
```bash
docker logs project
```

Manually load remote sspak
```bash
docker exec -it project sspak.load.remote
```

Manually save local sspak (will be stored in utils folder as local.sspak.phar)
```bash
docker exec -it project sspak.save.local
```
