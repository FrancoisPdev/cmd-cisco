# Sommaire
[Commandes](#cmd-cisco)

[Vocabulaires](#vocabulaires)

[Liens](#sources)

- - -
# Introduction
find a little list of command CISCO via CLI de certaine serie*

'show startup-config' (ou 'sh ru') : à utiliser le plus souvent possible.

'enable password _mot de passe_' - __mdp claire__

'enable secret _mot de passe_'  - __mdp hashé__

vlan : __802 1q__

trunk : __802 dot1q__

- - -
### cmd-cisco

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
[Sommaire](#sommaire)
- - -
# Vocabulaires

* __Carte d'interface réseau (NIC)__ - *Une NIC relie physiquement le dispositif terminal au réseau.*
* __Port physique__ - *Un connecteur ou une prise sur un dispositif de réseau où le support se connecte à un dispositif terminal ou à un autre dispositif de réseau.*
* __Interface__ - *Ports spécialisés sur un dispositif de réseau qui se connecte à des réseaux individuels. Comme les routeurs connectent les réseaux, les ports d'un routeur sont appelés interfaces de réseau.*
* __Schémas de topologie physique__ - *Les diagrammes de topologie physique illustrent l'emplacement physique des dispositifs intermédiaires et de l'installation des câbles. Vous pouvez voir que les pièces dans lesquelles se trouvent ces périphériques sont étiquetées dans la topologie physique.*
* __Schémas de topologie logique__ - *Les diagrammes de topologie logiques illustrent les périphériques, les ports et le schéma d'adressage du réseau. Vous pouvez voir quels périphériques terminaux sont connectés à quels périphériques intermédiaires et quels supports sont utilisés.*
* __Câble__ - *Généralement proposé par les fournisseurs de services de télévision par câble, le signal de données Internet est transmis sur le même câble que celui qui achemine la télévision par câble. Il offre une large bande passante, une grande disponibilité et une connexion permanente à l'internet.*
* __DSL__ - *Les lignes d'abonné numériques DSL offrent également une large bande passante, une grande disponibilité et une connexion permanente à l'internet. La technologie DSL utilise une ligne téléphonique. En général, un utilisateur de bureau à domicile ou de petit bureau se connecte à l'aide d'une ligne ADSL (Asymmetric Digital Subscriber Line), sur laquelle la vitesse descendante est supérieure à la vitesse ascendante.*
* __Cellulaire__ - *L'accès à Internet par téléphone cellulaire utilise un réseau de téléphonie mobile pour se connecter. Partout où vous captez un signal cellulaire, vous pouvez accéder à Internet. Les performances sont limitées par les capacités du téléphone et de la tour de téléphonie cellulaire à laquelle il est connecté.*
* __Satellite__ - *La disponibilité de l'accès à l'internet par satellite est un avantage dans les régions qui, autrement, n'auraient aucune connectivité internet. Les antennes paraboliques nécessitent une ligne de vue claire vers le satellite.*
* __Ligne commutée__ - *Une option peu coûteuse qui utilise n'importe quelle ligne téléphonique et un modem. La faible bande passante des connexions par ligne commutée n'est généralement pas suffisante pour les transferts de données importants, mais cette solution reste utile pour accéder à Internet lors d'un déplacement.*
* __Ligne louée dédiée__ - *Les lignes louées sont des circuits réservés au sein du réseau du fournisseur de services qui relient des bureaux géographiquement séparés pour un réseau privé de voix et/ou de données. Les circuits sont généralement loués sur une base mensuelle ou annuelle.*
* __Metro Ethernet__ - *Ceci est parfois connu sous le nom Ethernet WAN. Dans ce module, nous l'appellerons Metro Ethernet. Les Metro ethernets étendent la technologie d'accès au LAN au WAN. Ethernet est une technologie LAN que vous découvrirez dans un autre module.*
* __Business DSL__ - *Business DSL est disponible dans différents formats. Un choix populaire est la ligne d'abonné numérique symétrique (SDSL) qui est similaire à la version grand public de la DSL mais qui permet les téléchargements en amont et en aval aux mêmes vitesses élevées.*

- - - 
[Sommaire](#sommaire)
- - -
# Sources

[[Bit](https://fr.wikipedia.org/wiki/Bit)] -
[[TCP/UDP](https://en.wikipedia.org/wiki/List_of_TCP_and_UDP_port_numbers)] -
[[DSL](https://fr.wikipedia.org/wiki/Digital_subscriber_line#:~:text=Le%20terme%20Digital%20subscriber%20line,filaire%20t%C3%A9l%C3%A9phonique%20ou%20liaisons%20sp%C3%A9cialis%C3%A9es.)] -
[[OSI](https://fr.wikipedia.org/wiki/Modèle_OSI)] -
[[IPBX](https://fr.wikipedia.org/wiki/IPBX)] -
[[RFC](https://fr.wikipedia.org/wiki/Request_for_comments)] -
[[IETF](https://fr.wikipedia.org/wiki/Internet_Engineering_Task_Force)] -
[[ICANN](https://fr.wikipedia.org/wiki/Internet_Corporation_for_Assigned_Names_and_Numbers)] -
[[IAB](https://fr.wikipedia.org/wiki/Internet_Architecture_Board)]
