# cmd-cisco
find a little list of command CISCO via CLI de certaine serie*

'show startup-config' (ou 'sh ru') : à utiliser le plus souvent possible.

'enable password _mot de passe_' - __mdp claire__

'enable secret _mot de passe_'  - __mdp hashé__

vlan : __802 1q__

trunk : __802 dot1q__

- - -
# Security

### mdp console dans le CLI (sous cisco)
* en
* conf t
* line con 0
* username 'name' password 'console'
* login
* ctrl Z
* quitter la cession

### configurer son router (distance)
* conf t
* line vty 0 4
* username 'admin' password 'admin'
* login local
* end

# Description

### ajouter une description 
* en
* conf t
* int fa, vlan, etc...
* description "ma description"
* end

### Banner
* en
* conf t
* banner motd %
* Bonjour tout le monde %
* end

# Utility

### renomer un switch (sous CISCO)
* en
* conf t
* hostname '_mon_nom_'
* ctrl Z
* quitter la cession

# Vlan conf.

#### creer un vlan (sous CISCO)
* en
* conf t
* '_vlan X_'
* name '_mon_nom_'
* do sh ru
* ctrl Z

### Lier un (ou plusieurs) port dans un vlan (sous CISCO)
* conf t
* interface fa '0/x' | interface range fa '0/x-x'
* switch mode access
* switchport access '_mon_nom-de-vlan X_'
* do sh vlan
* ctrl Z

 ### créer des 'sub-interfaces' et leur attribuer un VLAN et une adresse IP. Cette interface deviendra le 'gateway' du VLAN (routeur CISCO)
* en
* int fa '0/x.X'
* encapsulation dot1Q 'X'
* ip address '192.168.1.254 255.255.255.0'
* ex

### attribuer un ip sur une interface vlan (sous CISCO)
* en
* conf t
* interface 'vlan x'
* ip address '192.168.1.100 255.255.255.0'
* no shutdown
* ctrl Z

### declarer un mode 'trunk' (etendre la communication des vlans de manière physique)
* conf t
* interface fa '0/x'
* switchport trunk encapsulation dot1q
* switchport mode trunk
* switchport trunk 'allow' vlan 'x-x' (ou juste vlan 'x'  pour une seul vlan)
* do sh ru
* crtl Z

# Save conf.

### enregistrer sa configuration
* en
* wr ou copy running-config startup-config

### balancer sa config (enregistré) sur un serveur
* en
* copy run tftp
* suivre les indications et valider
(il existe d'autre manip. avec CISCO)

### recuper sa conf.  sur le server
* en
* copy tftp start
* suivre les indications et valider
* reload

# Supprimer la conf. courante

### conf. à 0
* en
* write erase

- - - 
# Vocabulaires

* __Carte d'interface réseau (NIC)__ - *Une NIC relie physiquement le dispositif terminal au réseau.*
* __Port physique__ - *Un connecteur ou une prise sur un dispositif de réseau où le support se connecte à un dispositif terminal ou à un autre dispositif de réseau.*
* __Interface__ - *Ports spécialisés sur un dispositif de réseau qui se connecte à des réseaux individuels. Comme les routeurs connectent les réseaux, les ports d'un routeur sont appelés interfaces de réseau.*
* __Schémas de topologie physique__ - *Les diagrammes de topologie physique illustrent l'emplacement physique des dispositifs intermédiaires et de l'installation des câbles. Vous pouvez voir que les pièces dans lesquelles se trouvent ces périphériques sont étiquetées dans la topologie physique.*
* __Schémas de topologie logique__ - *Les diagrammes de topologie logiques illustrent les périphériques, les ports et le schéma d'adressage du réseau. Vous pouvez voir quels périphériques terminaux sont connectés à quels périphériques intermédiaires et quels supports sont utilisés.*


- - -
# Sources

[[Bit](https://fr.wikipedia.org/wiki/Bit)] -
[[TCP/UDP](https://en.wikipedia.org/wiki/List_of_TCP_and_UDP_port_numbers)] -
[[OSI](https://fr.wikipedia.org/wiki/Modèle_OSI)] -
[[IPBX](https://fr.wikipedia.org/wiki/IPBX)] -
[[RFC](https://fr.wikipedia.org/wiki/Request_for_comments)] -
[[IETF](https://fr.wikipedia.org/wiki/Internet_Engineering_Task_Force)]
