### VRRP & HSRP Projet ###
#-- Level : Intermediate --#
# Titre : {VRRP + HRSP} Cisco & Juniper
# Contexte : Le but de ce Lab est de déployer une infrastructure sur les technologies Cisco & Juniper principalement en garantissant une redondance par passerelle (HRSP sur Juniper et HSRP sur Cisco).
# OSPF a été utilisé comme IGP et BGP pour le Peering vers les Fournisseurs Internet Exchange ainsi que la redistribution des routes de BGP vers OSPF et de OSPF vers BGP.

# Objectifs
~ Assurer une bascule du traffic de R100 vers R200 en cas de non disponibilité de R100 qui est master VRRP et assurer le tracking des liens et routes.
~ Assurer une bascule du traffic de EDGE1 vers EDGE2 en cas de non disponibilité de EDGE1 qui est master HSRP et assurer le tracking des liens et routes
~ R100 & R200 sont les routeurs Juniper qui tournent sur OSPF 
~ EDGE1 & EDGE2 sont les routeurs Cisco ASBR qui font tourner du OSPF et BGP

# Difficulté & Rémédiation
--- Difficulté --- 
~ Le ping du Routeur Internet vers le PC vers PC Vlan10_User-1 ne passait pas
~ La bascule en cas d'interruption ne s'effectuait pas complètement, il y avait des routes qui n'étaient pas apprises et donc le traffic du Lan vers le Routeur Internet n'aboutissait pas
--- Rémédiation --- 
~ Création d'une règle d'autorisation des requêtes ICMP sur le parefeu Windows (Dans les prochains Labs , les stratégies GPO seront mises sur pieds pour pallier à certaines actions manuelles) , et le résultat a été positif : ping arrivé avec succès.
~ Vérification des configurations et après analyse , l'interface ae1 sur le R200 était configuré en ae0 , et la correction a été apportée sur la configuration de ae0 en ae1 et le device count a été augmenté sur R100 et R200 , le routage a été examiné à nouveau et tout était OK.

# Test
~ Coupure de R100 et Bascule effectuée sur R200 --> Success
~ Coupure de EDGE1 et Bascule effectuée sur EDGE2 --> Success
~ Ping de PC Vlan10_User-1 vers le Routeur Internet en fonctionnement nominal --> Success
~ Ping de PC Vlan10_User-1 vers le Routeur Internet en fonctionnement Bascule --> Success
~ Ping de PC Vlan10_User-1 vers les les différents hôtes du Réseau en fonctionnement nominal --> Success
~ Ping de PC Vlan10_User-1 vers les les différents hôtes du Réseau en fonctionnement Bascule --> Success

# Conclusion : 
Objectif atteint
