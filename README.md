# 🌐 Network Digital Twin & Automation Pipeline

![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Containerlab](https://img.shields.io/badge/Containerlab-Network_Simulation-green?style=for-the-badge)
![Ansible](https://img.shields.io/badge/Ansible-Configuration-red?style=for-the-badge&logo=ansible&logoColor=white)
![Netbox](https://img.shields.io/badge/Netbox-Source_of_Truth-blue?style=for-the-badge)
![Grafana](https://img.shields.io/badge/Grafana-Monitoring-orange?style=for-the-badge&logo=grafana&logoColor=white)

> **Projet d'Ingénierie DevOps & Réseau** : Conception d'un jumeau numérique (Digital Twin) pour simuler, automatiser et monitorer une infrastructure réseau critique.

---

## ⚠️ Avertissement de Confidentialité
*Ce projet a été réalisé dans un cadre professionnel soumis à une clause de confidentialité stricte. Le code présenté ici est une version **assainie et généralisée** (sanitized). Les données sensibles (topologies propriétaires, adressage IP interne, configurations de sécurité spécifiques) ont été retirées ou remplacées par des exemples génériques.*

---

## 📖 Contexte du Projet

Dans le but de moderniser les opérations réseau et de réduire les risques liés aux mises en production, ce projet vise à créer un **environnement de pré-production fidèle** (Jumeau Numérique). 

L'objectif était de passer d'une gestion manuelle et risquée à une approche **NetDevOps** complète : Infrastructure as Code (IaC), Source of Truth (SoT) et Observabilité.

### 🎯 Objectifs atteints
* **Réduction du temps de déploiement :** Passage de plusieurs heures à **~5 minutes**.
* **Fiabilisation :** Élimination des erreurs humaines grâce à la validation pré-déploiement.
* **Standardisation :** Utilisation de Netbox comme source unique de vérité.

---

## 🏗️ Architecture Technique

Le projet simule une architecture **Datacenter Spine-Leaf** (Clos Network) standard, entièrement conteneurisée.

### 🛠️ Stack Technologique

| Composant | Technologie | Rôle |
| :--- | :--- | :--- |
| **Orchestration** | **Containerlab** | Déploiement de la topologie réseau (noeuds et liens) sous forme de conteneurs. |
| **Virtualisation** | **Docker** | Exécution des routeurs virtuels (vEOS, cEOS ou images Linux génériques). |
| **Configuration** | **Ansible** | Gestion des configurations (Push) et templating (Jinja2). |
| **Source of Truth** | **Netbox** | Inventaire centralisé (IPAM, DCIM) pilotant l'automatisation. |
| **Monitoring** | **Grafana / Prometheus** | Tableaux de bord en temps réel (santé des liens, charge CPU/RAM). |
| **OS** | **Linux (Ubuntu)** | Environnement hôte et scripting Bash/Python. |

---

## 🔄 Workflow d'Automatisation

Le pipeline CI/CD mis en place suit les étapes suivantes :

1.  **Définition (Netbox) :** L'ingénieur définit l'état souhaité du réseau (nouveaux VLANs, sous-réseaux, équipements) dans Netbox.
2.  **Extraction (Python) :** Un script Python interroge l'API Netbox pour récupérer les données structurées.
3.  **Génération (Jinja2) :**
    * Génération dynamique du fichier de topologie `.clab.yml`.
    * Génération des fichiers de configuration initiaux des équipements.
4.  **Déploiement (Containerlab) :** Lancement automatique des conteneurs et câblage virtuel.
5.  **Provisioning (Ansible) :** Application des configurations avancées (OSPF/BGP, ACLs) via des playbooks Ansible.
6.  **Validation & Monitoring :** Tests de connectivité (PingMesh) et remontée des métriques vers Grafana.

---

## 🚀 Fonctionnalités Clés

* **Topologie Dynamique :** Capacité à déployer des architectures Spine-Leaf de taille variable (2 Spines / X Leafs) en changeant simplement les paramètres.
* **Zero-Touch Provisioning (Simulé) :** Les équipements démarrent avec une configuration de base injectée au boot.
* **Monitoring Intégré :** Les conteneurs sont automatiquement ajoutés à la cible Prometheus dès leur création.

---

## 📂 Structure du Répertoire (Exemple)

```text
.
├── ansible/
│   ├── inventory/          # Inventaire dynamique généré depuis Netbox
│   ├── playbooks/          # Playbooks de configuration (Routing, VXLAN...)
│   └── templates/          # Templates Jinja2 pour les configs switchs
├── containerlab/
│   ├── topologies/         # Fichiers .clab.yml
│   └── scripts/            # Scripts de post-démarrage
├── scripts/
│   ├── netbox_sync.py      # Synchro Netbox -> Local
│   └── topology_builder.py # Générateur de topologie
├── monitoring/
│   ├── prometheus/         # Configs Prometheus
│   └── grafana/            # Dashboards JSON exportés
└── README.md
