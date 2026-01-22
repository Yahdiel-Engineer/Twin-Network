# 🌐 Simulation Réseau Automatisée avec Containerlab

![Python](https://img.shields.io/badge/Python-3.8+-blue?logo=python&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-20.10+-blue?logo=docker&logoColor=white)
![Containerlab](https://img.shields.io/badge/Containerlab-0.40+-orange?logo=container&logoColor=white)
![Arista](https://img.shields.io/badge/Arista-cEOS-red?logo=cisco&logoColor=white)
![YAML](https://img.shields.io/badge/Config-YAML-yellow?logo=yaml&logoColor=black)
![Status](https://img.shields.io/badge/Status-Production-green)
![License](https://img.shields.io/badge/License-MIT-blue)

## 📋 Description du Projet

Ce projet développé durant un stage professionnel permet l'**automatisation complète de la simulation réseau** en utilisant Containerlab. Il combine monitoring temps réel des équipements physiques et génération dynamique de topologies virtuelles pour les tests et la formation.

Le système automatise la découverte de topologies réseau existantes, génère des environnements de simulation fidèles, et permet de tester des scénarios complexes (redondance, failover, changements de configuration) dans un environnement sécurisé et reproductible.

## ✨ Fonctionnalités Clés

🔍 **Monitoring Automatique**

- Surveillance temps réel des switches physiques via SNMP/SSH
- Détection automatique de la topologie réseau (LLDP)
- Collecte des configurations et états des équipements

🏗️ **Génération de Topologies**

- Création automatique de fichiers Containerlab YAML
- Déploiement d'environnements virtuels identiques au réseau physique
- Support des protocoles L2/L3 et des VLANs

🧪 **Tests et Simulation**

- Scénarios de test automatisés (spanning-tree, redondance)
- Simulation de pannes et tests de failover
- Validation de configurations avant déploiement

📊 **Visualisation**

- Génération de diagrammes réseau (Graphviz, Draw.io)
- Tableaux de bord de monitoring
- Rapports automatiques d'état

## 🛠️ Technologies Utilisées

| Catégorie                       | Technologies              |
| -------------------------------- | ------------------------- |
| **Conteneurisation** | Docker, Containerlab      |
| **Virtualisation Réseau** | Arista cEOS, Open vSwitch |
| **Automatisation** | Python 3.8+, Ansible      |
| **Gestion Réseau** | NAPALM, Netmiko, Paramiko |
| **Protocoles** | SNMP, SSH, LLDP, STP      |
| **Configuration** | YAML, Jinja2              |
| **Visualisation** | Graphviz, Matplotlib      |
| **Base de Données** | SQLite, JSON              |

## 🏗️ Architecture

```mermaid
graph TB
    A[Switches Physiques] --> B[Scripts de Monitoring]
    B --> C[Base de Données Local]
    C --> D[Générateur de Topologie]
    D --> E[Containerlab YAML]
    E --> F[Environnement Virtuel]
    F --> G[Tests Automatisés]
    G --> H[Rapports & Visualisation]
  
    subgraph "Environnement Docker"
        F
        I[cEOS Containers]
        J[Monitoring Tools]
    end
