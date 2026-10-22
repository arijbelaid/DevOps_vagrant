<div align="center">
  <h1>🚀 TP5 : Environnements de lab reproductibles avec Vagrant</h1>
  <p><strong>Combinaison de Vagrant (création des VMs) et Ansible (configuration)</strong></p>
  
  <img src="https://img.shields.io/badge/Vagrant-1563FF?style=for-the-badge&logo=vagrant&logoColor=white" alt="Vagrant" />
  <img src="https://img.shields.io/badge/VirtualBox-183A61?style=for-the-badge&logo=virtualbox&logoColor=white" alt="VirtualBox" />
  <img src="https://img.shields.io/badge/Ansible-EE0000?style=for-the-badge&logo=ansible&logoColor=white" alt="Ansible" />
  <img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white" alt="Docker" />
</div>

<br>

> **Objectif :** Créer un environnement de développement reproductible et léger. Le projet utilise un `Vagrantfile` multi-machines pour créer 2 VMs Ubuntu, puis utilise le provisioner Ansible pour installer Docker, Portainer, Jenkins et déployer l'application web conteneurisée (créée au TP4).

<div align="center">
  <br>
  📄 <strong><a href="./tp5_vagrant.pdf">Télécharger le rapport complet du TP5 (PDF)</a></strong>
  <br><br>
</div>

---

## 🛠️ Partie 0 : Prérequis et Installation

### Vérification de la Virtualisation Imbriquée
Pour que VirtualBox puisse fonctionner à l'intérieur de la VM de lab, la virtualisation imbriquée doit être activée. Le processeur expose bien les extensions (`vmx` / `svm`).

![Nested Virt](captures/01-nested-virt.png)

### Installation des Outils
Installation de VirtualBox, Ansible et Vagrant (via le dépôt HashiCorp) sur la VM de lab.

![Installation Outils](captures/02-install-outils.png)

---

## 🧪 Partie 1 : Démo Vagrant (Machine unique)

Création d'une première VM simple pour valider le fonctionnement de Vagrant. Le `Vagrantfile` synchronise un dossier local `web/` avec Apache et redirige le port 80 vers le port 8080.

### Le Vagrantfile de la démo
![Demo Vagrantfile](captures/03-demo-vagrantfile.png)

### Lancement de la VM
![Demo Vagrant Up](captures/04-demo-vagrant-up.png)

### Test du site web
Le site est accessible depuis le navigateur de la machine hôte sur le port 8080.

![Demo Web](captures/05-demo-web.png)

---

## 🌐 Partie 2 : Le Lab complet (Multi-machines)

Création d'un environnement avec **2 machines virtuelles** (`web1` et `web2`) sur un réseau privé (`private_network`). Chaque machine est configurée automatiquement via Ansible, qui réutilise les rôles du TP4.

### Préparation du projet
Récupération des rôles Ansible et des fichiers Docker depuis le dépôt du TP4.

![Lab Setup](captures/06-lab-setup.png)

### Le Playbook Ansible
Le playbook fait appel aux 3 rôles : `docker_portainer_install`, `jenkins_install` et `container_deployment`.

![Lab Playbook](captures/07-lab-playbook.png)

### Provisionnement avec Ansible
Exécution réussie des rôles sur les deux machines (`web1` et `web2`) avec `failed=0`.

![Lab Provision](captures/08-lab-provision.png)
![Lab Provision](captures/08-lab-provision1.png)


### État des machines
Les deux VMs sont lancées avec succès par Vagrant et sont en cours d'exécution.

![Lab Status](captures/09-lab-status.png)

### Services déployés
Les services sont accessibles depuis le navigateur de la machine hôte :
*   **Web1** : Site web (`8082`), Portainer (`9000`), Jenkins (`8081`)
*   **Web2** : Site web (`18082`), Portainer (`19000`), Jenkins (`18081`)

![Lab Services](captures/10-lab-services.png)
![Lab Services](captures/10-lab-services2.png)
![Lab Services](captures/10-lab-services3.png)
![Lab Services](captures/10-lab-services4.png)
![Lab Services](captures/10-lab-services5.png)


---
*Réalisé par [Arij Belaid](https://github.com/arijbelaid) dans le cadre du cours de DevOps.*
