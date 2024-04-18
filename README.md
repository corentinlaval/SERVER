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
- Besoin d'un service DHCP.

Il me faut donc une solution simple, gratuite, OpenSource, documentée, sur une plateforme accéssible et potentiellement graphique si un memebre de la startup souhaite paramétrer des accès et qu'elle ne si connait pas.

Je pars donc sur un routeur logiciel, un "ordinateur" avec un logiciel de routage et de firewall.

|  Nom  |  IPFire  |  VyOS  |  OpenWrt  |  PfSens  |  OpnSense  |
|---  |:-:  |:-:  |:-:  |:-:  |:-:  |
|  Plateformes  |  Linux  |  Linux  |  Linux  |  Toutes  |  Toutes  |
|  Prix  |  Gratuit  |  Gratuit puis payant  |  Gratuit  |  Gratuit  |  Gratuit  |
|  Support  |  En ligne  |  En ligne  |  En ligne  |  Appel  |  En ligne  |
|  Interface Graphique  |  Convaincante  |  Très convaincante  |  Convaincante  |  Convaincante  |  Très convaincante   |

> [!NOTE]
> Une interface graphique convaincante est attrayante et incite les utilisateurs à l'utiliser grâce à sa conception intuitive, son esthétique agréable et ses fonctionnalités engageantes.

Nous avons donc 2 solutions très similaires OpnSense et PfSense. Pour ce projet, j'ai donc décidé d'utiliser OpnSense, basé sur la partie graphique à mon gout plus attractive et une organisation des éléments, plus accessible.

> [!TIP]
> Lors d'un prochain projet, j'essaierai donc PfSense afin de "toucher à tout" et être polyvalent.

## 3-Installation du routeur

Après avoir mis les 2 barettes de RAM, la carte réseau et le SSD, j'ai pu mettre une clé USB sur le futur routeur.
Au préalable et à l'aide de BalenaEtcher, j'ai flashé une image OpenSense bootable sur ma clé afin de l'installer.
OpnSens à donc été installé sur la machine.

> [!IMPORTANT]
> Un compte root à été créé:
`Login: root`
`Password: root`

Enfin, après m'être connecté, j'ai créé mes interfaces.
> [!NOTE]
> Pour rappel un routeur à au minimum 2 interfaces réseau le LAN et le WAN.

Sur ma carte réseau, j'ai donc connecté un câble RJ45 entre l'interface igb0 et le switch. Ainsi qu'un second entre l'igb3 et le switch de l'entreprise vers le WAN et la connexion internet.
OpnSense donne la possibilité de les configurer, en donnant seulement l'interface.
Donnant par la suite ce schéma:

![Schéma réseau](https://github.com/corentinlaval/SERVER/blob/main/DiagProjet-3.png)

## 4-Accès à l'interface graphique

Une fois le routeur lancé, nous avons la possibilité d'accéder à l'interface graphique de celui-ci.
Il suffit de se connecter en filaire au switch du LAN, de forcer son adresse ip manuellement et la mettre sur le réseau. Enfin, nous pouvons accéder au routeur en allant avec le navigateur sur son adresse `192.168.1.1`.

> [!IMPORTANT]
> Pour rappel, les identifiants sont:
`Login: root`
`Password: root`
![Schéma réseau](https://github.com/corentinlaval/SERVER/blob/main/int)
>
![Schéma réseau](https://github.com/corentinlaval/SERVER/blob/main/int2)
>

## 5-Configuration du DHCP
> [!NOTE]
> Le service de DHCP est activé pour l'IPV4, il donnera une addresse automatiquement aux appareils connectés en filaire au réseau.
> Actuellement, la plage est laissée à l'initial, de `.100 à .199`, pour une structure de startup, une plage de 100 addresses est pour moi une solution amplement suffisante, mais peut-être modifiée.
> Deplus, la gateway, est donc l'adresse de l'interface interne du routeur soit 192.168.1.1. Pour le DNS, sans imposer d'adresse, c'est l'adresse par défaut qui est donnée. 
![https://github.com/corentinlaval/SERVER/blob/main/screenDHCP.png](https://github.com/corentinlaval/SERVER/blob/main/screenDHCP.png)
>

## 6-Firewall
> [!WARNING]
> Pour des raisons de securité, le FireWall est laissé comme à l'initial, activé reffusant tout accès de l'exterieur, il pourra par la suite être modifié selon les besoins.
![https://github.com/corentinlaval/SERVER/blob/main/FW)](https://github.com/corentinlaval/SERVER/blob/main/FW)
>

## 7-Intérêt de l'interface graphique
> [!TIP]
> L'interface graphique permet donc une modification plus "visuelle" des paramètres, mais donne aussi accès à de la suppervision et du monitoring réseau.
> Divers Dashboards sont disponibles et utiles dans la surveillance réseau. Comme les destinations de trames, le trafic des trames entrantes et sortantes...
![Schéma réseau](https://github.com/corentinlaval/SERVER/blob/main/dest)
>
![Schéma réseau](https://github.com/corentinlaval/SERVER/blob/main/graph)
>


## 8-Retour d'expérience
Ce projet m'a permit:
- [x] Une découverte, un apprentissage et une constatation des composants d'un ordinateur.
- [x] Une découverte et un apprentissage des routeurs logiciels.
- [x] Appliquer et approfondire mes connaissances dans le réseau et les routeurs logiciels.

