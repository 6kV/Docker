IP Adress of a container
-------------------------

sudo docker run -d --name nginx nginx
sudo docker inspect --format {{IpAdress}}nginx

sudo docker inspect --format '{{ .NetworkSettings.IPAddress}}' 09287
172.17.0.8

Network
--------

ifconfig : InterFace CONFIGurator (informations sur les interfaces réseau)
ifconfig peut aider à attribuer une adresse IP static à une interface réseau.
ip est une commande qui permet de faire la même chose que ifconfig (plus puissant).

iptables est un logiciel libre de l'espace utilisateur Linux grâce auquel l'administrateur système peut configurer les chaînes et règles dans le pare-feu en espace noyau (et qui est composé par des modules Netfilter).

netstat est une commande qui permet de connaitre toutes les connexions tcp sur une machine

Pour assigner une adresse réseau, il suffit d'indiquer l'adresse réseau après avoir précisé l'interface:

# ifconfig eth0 192.168.0.1

Assigner un masque de sous-réseau
Pour assigner le masque de sous-réseau, il faut utiliser l'option netmask suivit du masque à appliquer:

# ifconfig eth0 netmask 255.254.0.0
Généralement, le masque de sous-réseau est mis en même temps que l'adresse IP:

# ifconfig eth0 netmask 255.254.0.0 192.168.0.1

brctl is used to set up, maintain, and inspect the ethernet bridge con-
       figuration in the linux kernel.

NAT :
En réseau informatique, on dit qu'un routeur fait du Network Address Translation (NAT) (« translation d'adresse réseau »1) lorsqu'il fait correspondre les adresses IP internes non uniques et souvent non routables d'un intranet à un ensemble d'adresses externes uniques et routables. Ce mécanisme permet notamment de faire correspondre une seule adresse externe publique visible sur Internet à toutes les adresses d'un réseau privé, et pallie ainsi l'épuisement des adresses IPv4.



Network docker
--------------

Dés qu'on installe Docker, un brdige docker0 (interface réseau virtuelle) est créé.
une adresse ip lui est assigné avec un masque sous réseau disponible.



docker0   Link encap:Ethernet  HWaddr 00:00:00:00:00:00  
          adr inet6: fe80::ecc9:9fff:fe8e:24db/64 Scope:Lien
          UP BROADCAST MULTICAST  MTU:1500  Metric:1
          Packets reçus:11 erreurs:0 :0 overruns:0 frame:0
          TX packets:6 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 lg file transmission:0 
          Octets reçus:752 (752.0 B) Octets transmis:473 (473.0 B)
