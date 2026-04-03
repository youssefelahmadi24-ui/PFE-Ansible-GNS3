# 🚀 PFE 2026 : Automatisation de l'Infrastructure Réseau Agile (Ansible & GNS3)

**Réalisé par :** 
* **YASSINE EL GHAZI** (yassine.elghazi24@ump.ac.ma)
* **YOUSSEF EL AHMADI** (youssef.elahmadi24@ump.ac.ma)
* **NOUAMANE EL-JANHI** (nouamane.el-janhi24@ump.ac.ma)

## 📝 Description du Projet
Ce projet consiste à automatiser la configuration et la gestion d'une infrastructure réseau Cisco simulée sur **GNS3**. En utilisant **Ansible**, nous avons réussi à configurer plusieurs équipements (Routeurs et Switches) de manière centralisée, rapide et sans erreurs humaines.

### Objectifs atteints :
- Configuration automatique des Hostnames.
- Création et gestion des VLANs (Serveurs, Admin, Utilisateurs).
- Affectation dynamique des ports d'accès.
- Mise en place du routage dynamique **OSPF**.
- Configuration du protocole **SSH** pour la gestion à distance.
- Déploiement de serveurs **DHCP** pour l'adressage automatique.

---

## 🌐 Topologie du Réseau
L'infrastructure se compose de :
- **R1 & R2** : Routeurs Cisco 7200.
- **SW1** : Switch Cisco IOSvL2.
- **Clients** : PC Admin (VLAN 20), PC Utilisateur (VLAN 30), Zone DMZ/Serveur (VLAN 10).

![Topologie GNS3](topology.png)

---

## 🛠️ Guide d'Exécution (Les Commandes)

Pour lancer le projet, assurez-vous d'être dans le répertoire racine du projet et utilisez les commandes suivantes :

### 1. Vérification de la connectivité (Ping Ansible)
Avant de commencer, vérifiez que votre machine de gestion peut communiquer avec les équipements :

    ansible all -i hosts.ini -m ping
1. Lancement du déploiement global (Master Playbook)

    C'est la commande principale qui exécute toutes les configurations d'un seul coup (VLANs, Trunk, DHCP, OSPF) :

        ANSIBLE_HOST_KEY_CHECKING=False ansible-playbook -i hosts.ini master_pfe.yml

2. Lancement des modules spécifiques (Playbooks séparés)

    Si vous voulez lancer une partie précise de la configuration :

    Configuration du Switch (VLANs & SSH) :

        ANSIBLE_HOST_KEY_CHECKING=False ansible-playbook -i hosts.ini configure_switch.yml

    Configuration du Routage OSPF :

        ANSIBLE_HOST_KEY_CHECKING=False ansible-playbook -i hosts.ini ospf_config.yml

    Affectation des Ports aux VLANs :
        
        ANSIBLE_HOST_KEY_CHECKING=False ansible-playbook -i hosts.ini assign_ports.yml

3. Tests et Résultats*

    Voici comment nous avons validé le bon fonctionnement :

        Test          Commande de Vérification         Résultat Attendu

        VLANs         show vlan brief	               Les VLANs 10, 20 et 30 sont actifs sur SW1.

        Routage       show ip route ospf	           R1 et R2 connaissent les réseaux des VLANs via OSPF.

        DHCP          ip dhcp (sur VPCS)	           Les clients reçoivent une IP dans leur plage respective (192.168.x.0/24).
    
        Connectivité  ping 192.168.10.10	           Communication réussie entre les VLANs.# PFE-Ansible-GNS3