IP Adress of a container
-------------------------

    sudo docker run -d --name nginx nginx
    sudo docker inspect --format {{IpAdress}}nginx

    sudo docker inspect --format '{{ .NetworkSettings.IPAddress}}' 09287
    172.17.0.8
 
Linking container
------------------
    docker run -d --name database -e MY_SQL_ROOT_PASSWORD=root mysql
    docker run -d --link database:db --name web runseb/hostname
    docker run -d --link web:application --name lb nginx
  
The result of linking is that the application container now contains environment variables that point to the database.

    docker exec -ti web env | grep DB
    DB_PORT=tcp://172.17.0.13:3306
    ...
    DB_ENV_MY_SQL_VERSION=5.6.25

We can use these variables to dynamically configure the application.

the **/etc/hosts** file is also automatically updated to contain information for name resolution

    docker exec -ti web cat /etc/hosts
    172.17.0.14   62cba32....
    172.17.0.13   db ceab215b database
  
**If we restart a container, the /etc/hosts file of container that were linked to it will be updated, but env variables will be unchanged. Therefore using the content of /etc/hosts is the recommended way of extracting the IP adress of a linked container.**

We can use inspect command to see containers linking :

    docker inspect -f "{{.HostConfig.Links}}" application
    [/database:/application/db]
    
Although container linking is useful for development on a single machine, in large scale deployments it will show limitations, including when containers get restarted often. A system based on either DNS or dynamic container registration system will scale and be updated automatically.

Network docker
--------------

Dés qu'on installe Docker, un brdige **docker0** (interface réseau virtuelle) est créé.
une adresse ip lui est assigné avec un masque sous réseau disponible.



    **docker0** Link encap:Ethernet  HWaddr 00:00:00:00:00:00
    inet adr:172.17.42.1  Bcast:0.0.0.0  Masque:255.255.0.0
    UP BROADCAST MULTICAST  MTU:1500  Metric:1
    Packets reçus:11 erreurs:0 :0 overruns:0 frame:0
    TX packets:6 errors:0 dropped:0 overruns:0 carrier:0
    collisions:0 lg file transmission:0 
    Octets reçus:752 (752.0 B) Octets transmis:473 (473.0 B)


private address : 172.17.42.1
Masque sous réseau : 255.255.0.0

172.17.42.1/16

When a container is created, Docker creates a pair of "peer" network interfaces that are placed in two seperate network namespace: one interface in the networking namespace of the container (i.e eth0) and one interface in the networking namespace of the host, attached to the docker0 bridge.

In the container, a virtual network interface is created (**veth**) and attached to the bridge.
we can run this command to check bridge :
    brctl showu
    
Outbound networking traffic is forwarded to other interfaces of your docker host via IP forwarding and will go through NAT translation using an IP table masquerading rule.

Container Networking Namespace :
--------------------------------

 + --net=none : no networking namespace
 + --net=host : networking namespace of the host
 + --net=container:CONTAINER_ID : use network stack of another already running container




