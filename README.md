# Sommaire 
* [Reseaux en bref](#reseaux)
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
# Reseaux
Une suite de protocoles est un ensemble de protocoles qui fonctionnent ensemble pour fournir des services de communication réseau complets. Depuis les années 1970, il existe plusieurs suites de protocoles différentes, certaines développées par une organisation de normalisation et d'autres développées par divers fournisseurs.
Au cours de l'évolution des communications réseau et de l'Internet, il y avait plusieurs suites de protocoles concurrentes:
* __Internet Protocol Suite ou TCP/IP__ - Il s'agit de la suite de protocoles la plus courante et pertinente utilisée aujourd'hui. La suite de protocoles TCP/IP est une suite de protocoles standard ouverte gérée par Internet Engineering Task Force (IETF).
* __Protocoles d'interconnexion de systèmes ouverts (OSI)__ - Il s'agit d'une famille de protocoles élaborés conjointement en 1977 par l'Organisation internationale de normalisation (ISO) et l'Union internationale des télécommunications (UIT). Le protocole OSI comprenait également un modèle à sept couches appelé modèle de référence OSI. Le modèle de référence OSI classe les fonctions de ses protocoles. Aujourd'hui OSI est principalement connu pour son modèle en couches. Les protocoles OSI ont été largement remplacés par TCP/IP.
* __AppleTalk__ - Une suite de protocole propriétaire de courte durée publiée par Apple Inc. en 1985 pour les appareils Apple. En 1995, Apple a adopté TCP/IP pour remplacer AppleTalk.
* __Novell NetWare__ - Une suite de protocole propriétaire et un système d'exploitation réseau de courte durée développé par Novell Inc. en 1983 en utilisant le protocole réseau IPX. En 1995, Novell a adopté TCP/IP pour remplacer IPX.

TCP/IP est la suite de protocoles utilisée par Internet et les réseaux d'aujourd'hui. TCP/IP a deux aspects importants pour les fournisseurs et les fabricants :
* __Suite de protocoles standards ouverts__ - *Cela signifie qu'il est librement accessible au public et peut être utilisé par n'importe quel fournisseur sur son matériel ou dans son logiciel.*
* __Suite de protocoles basée sur des normes__ - *Cela signifie qu'elle a été approuvée par le secteur des réseaux et par un organisme de normalisation. Cela garantit que les produits de différents fabricants peuvent interagir avec succès.*


- - -
Le tableau énumère les différents types de protocoles nécessaires pour permettre les communications sur un ou plusieurs réseaux:

| Type de protocole	  | Description         |
| :--------------- | :--------------- |
| __Protocoles de Communications de Réseaux__	 | Les protocoles permettent à deux ou plusieurs périphériques de communiquer sur un ou plusieurs réseaux. La famille de technologies Ethernet implique une variété de protocoles tels que IP, Transmission Control Protocol (TCP), HyperText Transfer Protocol (HTTP), et bien d'autres encore. |
| __Protocoles de Sécurité des Réseaux__	 | Les protocoles sécurisent les données pour assurer l'authentification, l'intégrité des données et le cryptage des données. Exemples de protocoles sécurisés : Secure Shell (SSH), Secure Sockets Layer (SSL), et Transport Layer Security (TLS). |
| __Protocoles de Routage__	 | Les protocoles permettent aux routeurs d'échanger des informations de routage, de comparer les informations sur les chemins , puis pour sélectionner le meilleur chemin vers le réseau de destination. Exemples de protocoles de routage : Open Shortest Path First (OSPF) et Border Gateway Protocol (BGP). |
| __Protocoles de Découverte de Services__	 | Les protocoles sont utilisés pour la détection automatique des appareils ou des services. Exemples de protocoles de découverte de service : Dynamic Host Le protocole de configuration (DHCP) qui découvre des services pour l'attribution d'adresses IP , et le système de noms de domaine (DNS) qui est utilisé pour effectuer la traduction de noms en adresses IP. |
- - -
Les ordinateurs et les périphériques réseau utilisent des protocoles convenus pour communiquer. Le tableau énumère les fonctions de ces protocoles:

| Fonction  | Description         |
| :--------------- | :--------------- |
| __Adressage__ | Ceci identifie l'expéditeur et le destinataire prévu du message à l'aide d'un schéma d'adressage défini. Exemples de protocoles qui fournissent l'adressage comprend Ethernet, IPv4 et IPv6. |
| __La fiabilité__	 | Cette fonction offre des mécanismes de livraison garantis au cas où les messages seraient perdus ou corrompus pendant le transit. TCP offre une livraison garantie. |
| __Contrôle de flux__	 | Cette fonction garantit que les données circulent à un rythme efficace entre deux dispositifs de communication. TCP fournit des services de contrôle de flux. |
| __Séquençage__ | Cette fonction identifie de manière unique chaque segment de données transmis. Le dispositif récepteur utilise les informations de séquençage pour reconstituer l'information correctement. Ceci est utile si les segments de données sont perdus, retardée ou reçue en panne. TCP fournit des services de séquençage. |
| __Détection des erreurs__	 | Cette fonction est utilisée pour déterminer si les données ont été endommagées pendant la transmission. Divers protocoles qui fournissent la détection des erreurs comprennent: Ethernet, IPv4, IPv6 et TCP. |
| __Interface de l'Application__	 | Cette fonction contient des informations utilisées pour le processus à processus les communications entre les applications réseau. Par exemple, lors de l'accès à une page Web, les protocoles HTTP ou HTTPS sont utilisés pour communiquer entre le processus Web client et serveur. |

* __Hypertext Transfer Protocol (HTTP)__ - *Ce protocole régit la manière dont un serveur web et un client web interagissent. Le protocole HTTP décrit le contenu et la mise en forme des requêtes et des réponses échangées entre le client et le serveur. Les logiciels du client et du serveur web implémentent le protocole HTTP dans le cadre de l'application. Le protocole HTTP dépend d'autres protocoles pour gérer le transport des messages entre le client et le serveur.*
* __Transmission Control Protocol (TCP)__ - *Ce protocole gère les conversations individuelles. TCP est responsable de garantir la livraison fiable des informations et de gérer le contrôle du flux entre les appareils finaux.*
* __Protocole Internet (IP)__ - *Ce protocole est responsable de la remise des messages de l'expéditeur au destinataire. IP est utilisé par les routeurs pour transférer les messages sur plusieurs réseaux.*
* __Ethernet__ - *Ce protocole est responsable de la remise des messages d'une carte réseau à une autre carte réseau sur le même réseau local (LAN) Ethernet.*

- - -
# cmd-cisco
Une commande peut exiger un ou plusieurs arguments. Pour connaître les mots-clés et les arguments requis pour une commande, consultez la section sur la syntaxe des commandes. La syntaxe indique le modèle ou le format qui doit être utilisé lorsque vous saisissez une commande.
- - -
find a little list of command CISCO via CLI de certaine serie*

'show startup-config' (ou 'sh ru') : à utiliser le plus souvent possible.

'enable password _mot de passe_' - __mdp claire__

'enable secret _mot de passe_'  - __mdp hashé__

vlan : __802 1q__

trunk : __802 dot1q__
- - -
Légende du tableau

| Convention  | Description         |
| :--------------- | :--------------- |
| gras | Le texte en gras signale les commandes et mots-clés à saisir tels quels.|
| Italique | Le texte en italique signale les arguments pour lesquels des valeurs doivent être saisies. |
| [x] | Les crochets signalent un élément facultatif (mot-clé ou argument). |
| {x} | Les accolades signalent un élément requis (mot-clé ou argument). |
| [x {y | z }]	 | Les accolades et les lignes verticales encadrées par des crochets signalent un choix obligatoire, au sein d'un élément facultatif. Les espaces sont utilisés pour délimiter clairement les parties de la commande. |
- - -
Les exemples suivants illustrent les conventions utilisées pour documenter et utiliser les commandes IOS:

* __ping__ _ip-address_ - La commande est __ping__ et l'argument défini par l'utilisateur est l'adresse IP du périphérique de destination. Par exemple, __ping 10.10.10.5__.
* __traceroute__ _ip-address_ - La commande est traceroute et l'argument défini par l'utilisateur est l'adresse IP du périphérique de destination. Par exemple, __traceroute 192.168.254.254__.

Une aide contextuelle vous permet de trouver rapidement des réponses aux questions suivantes:

* Quelles commandes sont disponibles dans chaque mode de commande?
* Quelles commandes commencent par des caractères spécifiques ou un groupe de caractères?
* Quels arguments et mots clés sont disponibles pour des commandes particulières?

Pour afficher l'aide contextuelle, tapez simplement un point d'interrogation, __?__, dans le CLI.
- - -
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
- - -
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
* line VTY 0 4 (0 15)
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
* write erase ou erase startup-config

- - - 
[Sommaire](#sommaire)
- - -
# Vocabulaires

* __Carte d'interface réseau (NIC)__ - *Une NIC relie physiquement le dispositif terminal au réseau.*
* __ARP__ - *Protocole de résolution des adresses. Fournit un mappage d'adresse dynamique entre une adresse IPv4 et une adresse physique.*
* __NAT__ - *Traduction des Adresses de Réseau. Traduit les adresses IPv4 d'un réseau privé en adresses IPv4 publiques uniques au monde*
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
* __Contrôle de flux__ - *Ceci est le processus de gestion de la vitesse de transmission des données. Le contrôle de flux définit la quantité d'informations qui peuvent être envoyées et la vitesse à laquelle elles peuvent être livrées. Si une personne parle trop rapidement, l’autre personne éprouve des difficultés à entendre et à comprendre le message. Dans la communication réseau, il existe des protocoles réseau utilisés par les périphériques source et de destination pour négocier et gérer le flux d'informations.*
* __Délai de réponse__ - *Si une personne pose une question et qu’elle n’entend pas de réponse dans un délai acceptable, elle suppose qu’aucune réponse n’a été donnée et réagit en conséquence. La personne peut répéter la question ou continuer à converser. Les hôtes du réseau sont également soumis à des règles qui spécifient le délai d'attente des réponses et l'action à entreprendre en cas de délai d'attente dépassé.*
* __La méthode d'accès__ - *détermine le moment où un individu peut envoyer un message. Cliquez sur Lecture dans la figure pour voir une animation de deux personnes parlant en même temps, puis une "collision d'informations" se produit, et il est nécessaire que les deux personnes s'arrêtent et recommencent. De même, lorsqu'un périphérique souhaite transmettre sur un réseau local sans fil, il est nécessaire que la carte d'interface réseau WLAN (NIC) détermine si le support sans fil est disponible.*




### Il existe plusieurs menaces externes courantes pour les réseaux :
* __Virus, vers, et chevaux de Trois__ - *logiciels malveillants et code arbitraire s'exécutant sur un périphérique utilisateur.*
* __Spyware et adware__ - *Ce sont des types de logiciels qui sont installés sur l'appareil d'un utilisateur. Le logiciel recueille alors secrètement des informations sur l'utilisateur.*
* __Attaques du jour zéro__ - *Appelées aussi attaques de l'heure zéro, elles se produisent le premier jour où une vulnérabilité est connue.*
* __Attaques des acteurs de menace__ - *Une personne malveillante attaque les appareils des utilisateurs ou les ressources du réseau.*
* __Attaques par déni de service__ - *Ces attaques ralentissent ou bloquent les applications et les processus sur un périphérique réseau.*
* __Interception et vol de données__ - *Cette attaque permet de capturer des informations privées sur le réseau d'une organisation.*
* __Usurpation d'identité__ - *Cette attaque consiste à voler les identifiants de connexion d'un utilisateur afin d'accéder à des données privées*

### Deux fichiers système stockent la configuration des périphériques:
* __startup-config__ - Ceci est le fichier de configuration enregistré qui est stocké dans NVRAM. Ce fichier stocké dans la mémoire vive non volatile contient toutes les commandes qui seront utilisées au démarrage ou au redémarrage. La mémoire vive non volatile ne perd pas son contenu lors de la mise hors tension du périphérique.
* __running-config__ - Ceci est stocké dans la mémoire vive (RAM). Il reflète la configuration actuelle. Modifier une configuration en cours affecte immédiatement le fonctionnement d'un périphérique Cisco. La RAM est une mémoire volatile. Elle perd tout son contenu lorsque le périphérique est mis hors tension ou redémarré.

### Exigences Relatives au Protocole de Réseau:
En plus d'identifier la source et la destination, les protocoles informatiques et réseau définissent la manière dont un message est transmis sur un réseau. Les protocoles informatiques communs comprennent les exigences suivantes :
* Codage des messages
* Format et encapsulation des messages
* La taille du message
* Synchronisation des messages
* Options de remise des messages


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
