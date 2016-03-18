First example
--------------
    docker run busybox echo hello world
    sudo docker run -t -i ubuntu:14.04 /bin/bash (runner un bash dans un container)
    sudo docker rm $(sudo docker ps -a -q)


 sudo docker run -ti -v  /home/wazza/dev/:/home/wazza ubuntu:14.04 /bin/bash
 cd /home/wazza
 ls


-v sans path du host : on crée un Data container

sudo docker run -ti -v  /cookbook  ubuntu:14.04 /bin/bash
cd cookbook
touch new_file_created.txt

exit

sudo docker inspect -f {{.Volumes}} 35e0a6fbad7a
/var/lib/docker/vfs/dir/6b1ceb2f49fe0aa34e3e02535b50467e8

ls
new_file_created.txt
voir la commande --volumes-from
------
docker ps -a : show all containers (non running too)
docker images : show all images on host
docker rmi : remove image
docker exec : run a command in the container
docker inspect : Return low-level information on a container or image
docker cp : Copy files/folders from a container's filesystem to the host path


-d : lancer le container en background
--link : linker des containers entre eux
-v : mount volumes
-e: variables injecter
-i : interactive
-t : allocate a pseudo tty
-P: let docker choose the port on the host to map

Si on ne met pas de tag, on prend par défaut la latest image



Si besoin de plusieurs application dans un container, on peut utiliser supervisor

