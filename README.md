# cmd-cisco
find a little list of command CISCO via CLI de certaine serie*

'show startup-config' (ou 'sh ru') : à utiliser le plus souvent possible.
'enable password _mot de passe_' - __mdp claire__
'enable secret _mot de passe_'  - __mdp hashé__
vlan : __802 1q__
trunk : __802 dot1q__

# Security

### mdp console dans le CLI (sous cisco)
* en
* conf t
* line con 0
* password 'console'
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
* banner login %
* Bonjour tout le monde %
* end


# Utility

### renomer un switch (sous CISCO)
* en
* conf t
* host name '_mon_nom_'
* ctrl Z
* quitter la cession

# Vlan conf.

#### creer une vlan (sous CISCO)
* en
* conf t
* '_vlan 40_'
* hostname '_mon_nom_'
* do sh ru
* ctrl Z

### Lier une vlan dans un port (sous CISCO)
* conf t
* interface fa '0/x'
* switch mode access
* switchport access '_mon_nom-de-vlan_'
* do sh vlan
* ctrl Z

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
* switchport trunk allow vlan 'x-x' (ou juste vlan 'x'  pour une seul vlan)
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




