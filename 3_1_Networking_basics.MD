Network
--------

**TCP** : est un protocole de transport fiable, en mode connecté. (établissement d'une session de communication entre deux parties qui veulent échanger des données. Cette session comporte un début, une fin et une validation (vérification des erreurs), classiquement un identifiant un mot de passe)

**UDP** : Contrairement au protocole TCP, il fonctionne sans négociation : il n'existe pas de procédure de connexion préalable à l'envoi des données (le handshaking). Donc UDP ne garantit pas la bonne livraison des datagrammes à destination, ni leur ordre d'arrivée. Il est également possible que des datagrammes soient reçus en plusieurs exemplaires.
Il est utilisé quand il est nécessaire soit de transmettre des données très rapidement, et où la perte d'une partie de ces données n'a pas grande importance, soit de transmettre des petites quantités de données, là où la connexion « 3-WAY » TCP serait inutilement coûteuse en ressources. Par exemple, dans le cas de la transmission de la voix sur IP, la perte occasionnelle d'un paquet est tolérable dans la mesure où il existe des mécanismes de substitution des données manquantes, par contre la rapidité de transmission est un critère primordial pour la qualité d'écoute.
Exple d'utilisation : streaming, jeux en réseau...

Il est également utilisé pour émettre des données à plusieurs récepteurs simultanément (multicast, broadcast), la connexion TCP n'étant que point-à-point.

**FQDN** : Dans le DNS, un fully qualified domain name (FQDN, ou nom de domaine complètement qualifié) est un nom de domaine qui révèle la position absolue d'un nœud dans l'arborescence DNS en indiquant tous les domaines de niveau supérieur jusqu'à la racine. On parle également de domaine absolu, par opposition aux domaines relatifs. Par convention, le FQDN est ponctué par un point final

exemples : 
 + commons.wikimedia.org. est un FQDN car aucun sous-domaine supérieur n'est omis et il se termine par un point final.
 + commons et commons.wikimedia ne sont pas des FQDN car les domaines de niveau supérieur sont omis.

**/etc/hosts** : Le fichier hosts est utilisé sous tous les systèmes d’exploitations lors de l’accès à Internet, ce fichier est consulté avant l’accès au serveur DNS. C’est un simple fichier qui contient sur la même ligne une adresse IP et parfois le nom de domaine. Ce fichier peut aussi servir à définir les noms des machines sur un réseau local.

    ifconfig : InterFace CONFIGurator (informations sur les interfaces réseau)

**ifconfig** peut aider à attribuer une adresse IP static à une interface réseau.
    
    **ip** est une commande qui permet de faire la même chose que ifconfig (plus puissant).

**iptables** permet de configurer les chaînes et règles dans le pare-feu en espace noyau (et qui est composé par des modules Netfilter).

**netstat** est une commande qui permet de connaitre toutes les connexions tcp sur une machine

Pour assigner une adresse réseau, il suffit d'indiquer l'adresse réseau après avoir précisé l'interface:

    ifconfig eth0 192.168.0.1

Assigner un masque de sous-réseau
Pour assigner le masque de sous-réseau, il faut utiliser l'option netmask suivit du masque à appliquer:

    ifconfig eth0 netmask 255.254.0.0

Généralement, le masque de sous-réseau est mis en même temps que l'adresse IP:

    fconfig eth0 netmask 255.254.0.0 192.168.0.1

**brctl** is used to set up, maintain, and inspect the ethernet bridge configuration in the linux kernel.
An ethernet bridge is a device commonly used to connect different  networks of ethernets together, so that these ethernets will appear as one ethernet to the participants.

    brctl show
    bridge name	bridge id		STP enabled	interfaces
    docker0		8000.000000000000	no		
    lxcbr0		8000.000000000000	no		



NAT
-----

En réseau informatique, on dit qu'un routeur fait du Network Address Translation (NAT) (« translation d'adresse réseau ») lorsqu'il fait correspondre les adresses IP internes non uniques et souvent non routables d'un intranet à un ensemble d'adresses externes uniques et routables. Ce mécanisme permet notamment de faire correspondre une seule adresse externe publique visible sur Internet à toutes les adresses d'un réseau privé, et pallie ainsi l'épuisement des adresses IPv4.

