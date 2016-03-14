keeping changes made to a container :
-------------------------------------

docker run -ti ubuntu:14.04 /bin/bash
root@34b32e:/# sudo apt-get update

....

docker commit 34b32e ubuntu:latest

docker images (you will find the new images created)

to check modification done to a container
docker diff 34b32e

import/export containers
-------------------------

docker ps -a
docker export 34b32e > update.tar
docker import - update < update.tar

Dockerfile
-----------

From : image de base8ices
---------------
https://docs.docker.com/engine/userguide/eng-image/dockerfile_best-practices/

Single process per container (decoupled application that can scale)
your containers are ephemeral : u shouldn't modify them, manage configuration and data outside the container
use .dockerignore file when building images
use official images
minimize the number of layers of your images


