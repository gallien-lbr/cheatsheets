# Memo Réseau Notes diverses

## Adresse IP v4

Une adresse IPv4 est composée de 32 bits.

Une adresse IP se compose de deux parties :

- L'adresse réseau est une série de chiffres pointant vers l'identifiant unique du réseau. 
- L'adresse de l'hôte est une série de chiffres indiquant l'identifiant de l'hôte ou du périphérique individuel sur le réseau.

Jusqu'au début des années 1990, les adresses IP étaient attribuées à l'aide du système d'adressage par classes.

## Adresse sans classe ou CIDR

Les adresses sans classe ou de routage inter-domaines sans classe (CIDR) utilisent le masque de sous-réseaux à longueur variable (VLSM, variable length subnet masking) pour modifier le rapport entre les bits d'adresse réseau et hôte dans une adresse IP. 

* Classless Inter-Domain Routing, ou en fr : routage inter-domaines sans classe (CIDR)
* Exemple adresse en notation CIDR
**192.0.2.0/24** => ici les 24 premiers bits correspondent à l'adresse réseau
