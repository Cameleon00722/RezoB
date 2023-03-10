# RezoB

Devoir de TP de L3 Réseaux

L'objectif de ce devoir, à réaliser seul ou en binôme, est de configurer le réseau proposé pour qu'alice puisse accéder à la page web www.notascam.com : configuration des interfaces, des routes, DHCP, DNS, NAT, RIP. 

== The big picture ==
Vous disposez d'un bloc d'adresses donné en paramètre que vous utiliserez pour le réseau sur lequel se trouvent alice et boxa, pour le réseau sur lequel se trouvent www, dnsnot, mailnot et boxb, et pour le réseau central où sont connectés rtw, rtx, rty et rtz.

Vous utiliserez comme paramètre (bloc d'adresses privées) le paramètre proposé sur celene pour l'un ou l'autre des membres du binôme.

Les 4 routeurs rtw, rtx, rty et rtz constituent le coeur du réseau et feront transiter l'ensemble des communications IP.

Il est interdit de modifier "lab.conf", la structure du réseau ne doit pas être modifiée !

== Ce qui est à configurer ==

Seuls sont à modifier les fichiers :
- boxa.startup et boxb.startup
- boxa/etc/dhcp/dhcpd.conf et boxb/etc/dhcp/dhcpd.conf 
- rti.startup où rti peut valoir rtw, rtx, rty ou rtz
- rti/etc/frr/ripd.conf où rti peut valoir rtw, rtx, rty ou rtz
- dnsnot/etc/bind/file où file peut valoir named.conf ou db.com.notascam

Votre travail consiste à configurer les machines et services suivants :
- configuration IP des interfaces eth0 de boxa et boxb. On utilisera des adresses dans le bloc d'adresses pris comme paramètre.
- service DHCP sur boxa pour qu'alice obtienne les informations nécessaires. On proposera '20.30.40.50' comme résolveur DNS.
- service DHCP sur boxb pour que www, mailnot et dnsnot soient connectés, chacun avec une IP fixe. On proposera toujours '20.30.40.50' comme résolveur DNS et "notascam.com" comme nom de domaine.
- services de NAT sur boxa et boxb pour qu'alice puisse communiquer hors de son réseau privé, et pour que :
  * les requêtes HTTP puissent arriver jusqu'à www
  * les requêtes DNS puissent arriver jusqu'à dnsnot
  * les connexions SMTP puissent atteindre mailnot.
- routage RIP sur rtw, rtx, rty et rtz pour que ces 4 routeurs obtiennent des routes vers tous les réseaux présents. On pourra soit configurer les interfaces en passant par zebra, soit le faire dans les fichiers .startup. On peut par exemple se connecter à rtw sur le port ripd par telnet depuis alice, sauvegarder la configuration choisie puis la copier dans les répertoires de rtx, rty et rtz.
 ATTENTION à modifier les timers RIP : commande "timers basic 5 15 10" une fois connecté au démon ripd.
- service d'administration DNS de la zone notascam par la machine dnsnot. La base de données DNS de dnsnot doit contenir les adresses de www, mailnot et dnsnot, ainsi que des enregistrements de type NS (vers dnsnot) et MX (vers smtp.notascam.com).

 
== Modalités de retour du devoir ==

Le devoir est à traiter en binôme (ou monôme). La solution est à déposer sous la forme d'une archive nommée nom1.prenom1_nom2.prenom2.tar.gz sur la page Celene du cours avant le 8/1/23 à 23h59. 

L'archive doit contenir :
 - un rapport au format PDF qui reprend les noms des membres du binôme, le paramètre utilisé et qui explique très brièvement le travail effectué.
 - le lab modifié par vos soins.
