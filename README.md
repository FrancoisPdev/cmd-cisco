# cmd-cisco
find a little list of command CISCO via CLI 

'enable password _mot de passe_' - __mdp claire__
'enable secret _mot de passe_'  - __mdp hashé__
vlan : __802 1q__
trunk : __802 dot1q__

mdp console dans le CLI (sous cisco)
* en
* conf t
* line con 0
* password 'console'
* login
* ctrl Z
* quitter la cession

 renomer un switch (sous CISCO)
* en
* conf t
* host name '_mon_nom_'
* ctrl Z
* quitter la cession

creer une vlan (sous CISCO)
* en
* conf t
* '_vlan 40_'
* name '_mon_nom_'
* do sh ru
* hostname '_mon_nom_'
* do sh ru
* ctrl Z

Lier un vlan dans un port (sous CISCO)
* conf t
* interface fa 0/1
* switch mode access
* switchport access '_mon_nom-de-vlan_'
* do sh vlan
* ctrl Z

attribuer un ip sur une interface vlan (sous CISCO)
* en
* conf t
* interface vlan 1
* ip address192.168.1.100 255.255.255.0
* no shutdown
* ctrl Z

declarer un mode 'trunk' (etendre la communication des vlans)
* conf t
* interface fa 0/2
* switchport mode trunk
* do sh ru
* crtl Z

configurer son router (distance)
* conf t
* username 'admin' password 'admin'
* line vty 0 4
* login local
* end













