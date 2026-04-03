🚀 PFE 2026 : Automatisation de l'Infrastructure Réseau Agile (Ansible & GNS3)

Réalisé par :

YASSINE EL GHAZI (yassine.elghazi24@ump.ac.ma)

YOUSSEF EL AHMADI (youssef.elahmadi24@ump.ac.ma)

NOUAMANE EL-JANHI (nouamane.el-janhi24@ump.ac.ma)

📝 Description du Projet

Ce projet consiste à automatiser la configuration et la gestion d'une infrastructure réseau Cisco simulée sur GNS3. En utilisant Ansible, nous avons réussi à configurer plusieurs équipements (Routeurs et Switches) de manière centralisée, rapide et sans erreurs humaines.

Objectifs atteints :

Configuration automatique des Hostnames.

Création et gestion des VLANs (Serveurs, Admin, Utilisateurs).

Affectation dynamique des ports d'accès.

Mise en place du routage dynamique OSPF.

Configuration du protocole SSH pour la gestion à distance.

Déploiement de serveurs DHCP pour l'adressage automatique.

📦 Prérequis & Équipements (Images GNS3)

Pour reproduire cette topologie, vous devez importer les images suivantes dans votre environnement GNS3. Voici les versions exactes utilisées dans ce projet :

Équipement

Version Exacte

Type de Fichier

Lien de Référence / Téléchargement

Routeur (R1, R2)

c7200-adventerprisek9-mz.124-24.T8.bin

Dynamips (.bin)

Cisco 7200 Appliance

Switch L2 (SW1)

vios_l2-adventerprisek9-m.ssa.high_iron_20200929.qcow2

QEMU (.qcow2)

Cisco IOSvL2 Appliance

Serveur/Client

debian-12.6.qcow2

QEMU (.qcow2)

Debian Official Cloud Images

Routeur IOSv

vios-adventerprisek9-m.vmdk.SPA.156-2.T.qcow2

QEMU (.qcow2)

Cisco IOSv Appliance

Note : Les images Cisco IOS sont protégées par copyright. Vous devez posséder une licence Cisco valide pour les utiliser légalement.

🌐 Topologie du Réseau

L'infrastructure se compose de :

R1 & R2 : Routeurs Cisco 7200.

SW1 : Switch Cisco IOSvL2.

Clients : PC Admin (VLAN 20), PC Utilisateur (VLAN 30), Zone DMZ/Serveur (VLAN 10).

🛠️ Guide d'Exécution (Les Commandes)

Pour lancer le projet, assurez-vous d'être dans le répertoire racine du projet et utilisez les commandes suivantes :

1. Vérification de la connectivité (Ping Ansible)

ansible all -i hosts.ini -m ping


2. Lancement du déploiement global (Master Playbook)

ANSIBLE_HOST_KEY_CHECKING=False ansible-playbook -i hosts.ini master_pfe.yml


3. Mise à jour du projet (Git Workflow)

Pour enregistrer vos modifications et les envoyer sur GitHub :

git add .
git commit -m "Description de vos modifications"
git pull origin main --rebase
git push origin main


✅ Tests et Résultats

Voici comment nous avons validé le bon fonctionnement de l'infrastructure :

Test

Commande de Vérification

Résultat Attendu

VLANs

show vlan brief

Les VLANs 10, 20 et 30 sont actifs sur SW1.

Routage

show ip route ospf

R1 et R2 connaissent les réseaux des VLANs via OSPF.

DHCP

ip dhcp (sur VPCS)

Les clients reçoivent une IP dans leur plage respective (192.168.x.0/24).

Connectivité

ping 192.168.10.10

Communication réussie entre les VLANs.