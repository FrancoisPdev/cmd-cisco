# Sommaire 
* [Commandes](#cmd-cisco)
* [Security](#security)
* [Description](#description)
* [Utility](#utility)
* [VLAN](#vlan-conf)
* [Save](#save-conf)

[Vocabulaires](#vocabulaires)

[Liens](#sources)

- - -
# Introduction

Quand j'ai créé ce dépôt, c'était pour garder une trace de mon apprentissage. Ceci restera un petit coin, public, où l'on pourra peut-être pécho des informations ! Il existe d'excellents programmes d'émulation de terminal permettant de se connecter à un périphérique réseau via une connexion série sur un port de console ou via une connexion SSH ou Telnet.

Par mesure de sécurité, le logiciel Cisco IOS sépare l'accès à la gestion en deux modes de commande:

* Mode d'exécution utilisateur - ce mode offre des fonctionnalités limitées, mais s'avère utile pour les opérations de base. Il autorise seulement un nombre limité de commandes de surveillance de base, mais il n'autorise aucune commande susceptible de modifier la configuration du périphérique. Le mode d'exécution utilisateur se reconnaît à l'invite CLI qui se termine par le symbole >.

* Mode d'exécution privilégié - pour exécuter les commandes de configuration, un administrateur réseau doit accéder au mode d'exécution privilégié. Pour accéder aux modes de configuration supérieurs, comme celui de configuration globale, il est nécessaire de passer par le mode d'exécution privilégié. Le mode d'exécution privilégié se reconnaît à l'invite qui se termine par le symbole # .

Les directives pour la configuration des noms d'hôte sont répertoriées ci-dessous:
* débutent par une lettre
* Ne contiennent pas d'espaces
* se terminent par une lettre ou un chiffre
* Ne comportent que des lettres, des chiffres et des tirets
* Comportent moins de 64 caractères

Différentes commandes sont utilisées pour entrer et sortir des invites de commandes. Pour passer du mode utilisateur au mode privilégié, utilisez la commande __enable__ . Utilisez la commande __disable__ du mode d'exécution privilégié pour retourner au mode d'exécution utilisateur.

Pour passer de n'importe quel sous-mode de configuration du mode de configuration globale au mode situé un niveau plus haut dans la hiérarchie des modes, saisissez la commande __exit__ .

Pour passer de n'importe quel sous-mode de configuration au mode d'exécution privilégié, entrez la commande __end__ ou utilisez la combinaison de touches __Ctrl+Z__

Vous pouvez aussi passer directement d'un sous-mode de configuration à un autre. Notez qu'après avoir sélectionné une interface, l'invite de commande change de __(config-line)#__ à __(config-if)#__.

_N'oubliez pas de mettre à jour la documentation chaque fois que vous ajoutez ou modifiez un périphérique. Dans la documentation, identifiez les périphériques par leur emplacement, leur rôle et leur adresse._
- - -
find a little list of command CISCO via CLI de certaine serie*

'show startup-config' (ou 'sh ru') : à utiliser le plus souvent possible.

'enable password _mot de passe_' - __mdp claire__

'enable secret _mot de passe_'  - __mdp hashé__

vlan : __802 1q__

trunk : __802 dot1q__

- - -
### cmd-cisco
Légende du tableau

| Touche  | Description          |
| :--------------- | :--------------- |
| Tabulation  | 	Complète un nom de commande entré partiellement.|
| Retour |  arrière	Efface le caractère à gauche du curseur.|
| Ctrl+D | 	Efface le caractère à l'emplacement du curseur. |
| Ctrl+K |  	Efface tous les caractères à partir du curseur jusqu'à la fin de la ligne de commande.|
| Échap D | 	Efface tous les caractères à partir du curseur jusqu'à la fin du mot.|
| Ctrl+U   |	Efface tous les caractères à partir du curseur jusqu'au début de la ligne de commande.|
| ou Ctrl+X |	Efface le mot à gauche du curseur.|
| Ctrl+W| Déplace le curseur vers le début de la ligne.|
| Ctrl+A	|Touche fléchée vers la gauche ou Ctrl+B	Déplace le curseur d'un caractère vers la gauche. |
| Échap B |Déplace le curseur d'un mot vers la gauche.|
| Échap F | 	Déplace le curseur d'un mot vers la droite.|
| Flèchedroite ou Ctrl+F |Déplace le curseur d'un caractère vers la droite.|
| Ctrl+E|	Déplace le curseur vers la fin de la ligne.|
| Haut ou Ctrl+P |Rappelle les commandes antérieures en commençant par les plus récentes.|
| Ctrl+R ou Ctrl+I ou Ctrl+L|	Rappelle l'invite du système et la ligne interrompue par la réception d'un message IOS.|

| Touche  | Description          |
| :--------------- | :--------------- |
| Touche Entrée	 |Affiche l'écran suivant.|
| Barre d'espace	 |Termine la chaîne d'affichage et revient au mode d'exécution privilégié.|
| Toute autre clé	 | Termine la chaîne d'affichage et revient au mode d'exécution privilégié |

Ce tableau répertorie les commandes utilisées pour quitter une opération:
| Touche  | Description          |
| :--------------- | :--------------- |
| Ctrl+C	 | Dans un mode de configuration, permet de quitter le mode de configuration et de retourner au mode d'exécution privilégié. à partir du mode d'exécution, l'invite reparaît .|
| Ctrl+Z	 | Dans un mode de configuration, permet de quitter le mode de configuration et de retourner au mode d'exécution privilégié.|
| __Ctrl+Maj+6__	 | Séquence d'interruption permettant d'abandonner les recherches DNS, traceroutes, pings, etc.|


# Security
Utilisez des mots de passe forts qui ne sont pas faciles à deviner. Pour choisir les mots de passe, respectez les règles suivantes:

* Utilisez des mots de passe de plus de 8 caractères.
* Utilisez une combinaison de lettres majuscules et minuscules, des chiffres, des caractères spéciaux et/ou des séquences de chiffres.
* Évitez d'utiliser le même mot de passe pour tous les périphériques.
* N'utilisez pas des mots courants car ils sont faciles à deviner.

###### Utilisez une recherche sur Internet pour trouver un générateur de mot de passe. 

### mdp console dans le CLI (sous cisco)
* en
* conf t
* line con 0
* username 'name' password 'console'
* login
* ctrl Z
* quitter la cession

### sécuriser l'accès au mode d'exécution privilégié
* en
* conf t
* enable secret 'mot de passe'
* exit

### configurer son router (distance)
* en
* conf t
* line vty 0 4 (0 15)
* username 'admin' password 'admin'
* login
* end

###  chiffrer tous les mots de passe en texte clair
* en
* conf t
* 'service password-encryption'

- - -
# Description

### ajouter une description 
* en
* conf t
* int fa, vlan, etc...
* description "ma description"
* end

### Banner (MOTD (Message Of The Day))
* en
* conf t
* banner motd % ou #
* Bonjour tout le monde %/#
* end
###### Les bannières peuvent constituer une pièce importante dans un procès intenté à une personne qui aurait accédé illégalement à un périphérique.
- - -
# Utility

### renomer un switch (sous CISCO)
* en
* conf t
* hostname '_mon_nom_'
* ctrl Z
* quitter la cession

### Configurez l'horloge
* en
* clock set? (Le point d'interrogation (?) fournit une aide et vous permet de
déterminer le mode de saisie attendu pour configurer l'instruction)
* show clock (pour verifier les paramètres.)
- - -
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
- - -
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
- - -
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
* __Redondance__ - *Le fait de disposer de plusieurs chemins vers une destination*
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
* __Confidentialité__ - *La confidentialité des données signifie que seuls les destinataires prévus et autorisés peuvent accéder aux données et les lire.*
* __Intégrité__ - *L'intégrité des données garantit aux utilisateurs que les informations n'ont pas été altérées lors de leur transmission, de l'origine à la destination.*
* __Disponibilité__ - *La disponibilité des données garantit aux utilisateurs un accès rapide et fiable aux services de données pour les utilisateurs autorisés*

### Il existe plusieurs menaces externes courantes pour les réseaux :
* __Virus, vers, et chevaux de Trois__ - *logiciels malveillants et code arbitraire s'exécutant sur un périphérique utilisateur.*
* __Spyware et adware__ - *Ce sont des types de logiciels qui sont installés sur l'appareil d'un utilisateur. Le logiciel recueille alors secrètement des informations sur l'utilisateur.*
* __Attaques du jour zéro__ - *Appelées aussi attaques de l'heure zéro, elles se produisent le premier jour où une vulnérabilité est connue.*
* __Attaques des acteurs de menace__ - *Une personne malveillante attaque les appareils des utilisateurs ou les ressources du réseau.*
* __Attaques par déni de service__ - *Ces attaques ralentissent ou bloquent les applications et les processus sur un périphérique réseau.*
* __Interception et vol de données__ - *Cette attaque permet de capturer des informations privées sur le réseau d'une organisation.*
* __Usurpation d'identité__ - *Cette attaque consiste à voler les identifiants de connexion d'un utilisateur afin d'accéder à des données privées*
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
