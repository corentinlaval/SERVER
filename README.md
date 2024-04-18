# Projet Corp Unlimited - Mise en place du réseau
# Situation
Emménagement d'une nouvelle Startup, je suis en charge de la configuration et de la mise en place du réseau interne de l'établissement.

# Objectif: 
Réaliser un réseau LAN pour l'entreprise, pouvant accéder au WAN de manière fiable et sécurisée.

# Matériel à disposition:
- HP Compaq 6005 Pro (AMD Athlon(tm) II X2 B28 Processor) : 2*3.4 Ghz + 2 Go Ram DDR3 + HDD 256 Go (Boot F9 - BIOS F10)
- Switch Cisco Catalyst 2950-24 Switch 24 10/100 ports
- Ordinateurs

## 1-Réalisation du schéma réseau

Après reflexion, le réseau est assez simple à mettre en place, composé d'un switch (permettant les trafics inter LAN) et d'un routeur autorisant une communication entre LAN et WAN.
Deplus, il est demandé de s'intéresser sur l'option sécurité du réseau, il nous faut donc un Firewall. 
La schéma revient à 2 solution données ci-dessous:

![Schéma réseau](https://github.com/corentinlaval/SERVER/blob/main/RéseauProj.png)

Une solution avec un routeur et un Firewall ou une solution intégrant les 2 en une seule entitée.

## 2-Choix du routeur

Après un point sur ma situation:
- En période d'éssai --> Solution maintenable pour les futurs employés si ce n'est pas moi.
- Startup --> Budget potentiellement restreint, préférer les open sources.

Il me faut donc une solution simple, gratuite, OpenSource, documentée, sur une plateforme accéssible et potentiellement graphique si un memebre de la startup souhaite paramétrer des accès et qu'elle ne si connait pas.

Je pars donc sur un routeur logiciel, un "ordinateur" avec un logiciel de routage et de firewall.

|  Nom  |  IPFire  |  VyOS  |  OpenWrt  |  PfSens  |  OpnSense  |
|---  |:-:  |:-:  |:-:  |:-:  |:-:  |
|  Plateformes  |  Linux  |  Linux  |Linux  |  Toutes  |  Toutes  |
|  Prix  |  Gratuit  |  Gratuit au début puis payant  |Gratuit  |  Gratuit  |  Gratuit  |
|  Support  |  En ligne  |  En ligne ++ (24/7)  |En ligne  |  Appel  |  En ligne  |
|  Interface Graphique  |  Compréhensible  |  Très compréhensible  |Compréhensible  |  Compréhensible  |  Très compréhensible   |

Nous avons donc 2 solutions très similaires OpnSense et PfSense. Pour ce projet, j'ai donc décidé d'utiliser OpnSense, basé sur la partie graphique à mon gout plus attractive et une organisation des éléments, plus accessible.

> [!TIP]
> Lors d'un prochain projet, j'essaierai donc PfSense afin de "toucher à tout" et être polyvalent.
