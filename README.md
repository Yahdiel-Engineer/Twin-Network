# 🌐 Network Digital Twin & Automation Pipeline

<div align="center">

![Status](https://img.shields.io/badge/Status-Sanitized_Demo-success?style=for-the-badge)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Containerlab](https://img.shields.io/badge/Containerlab-Network_Simulation-green?style=for-the-badge)
![Ansible](https://img.shields.io/badge/Ansible-Configuration-red?style=for-the-badge&logo=ansible&logoColor=white)
![Python](https://img.shields.io/badge/Python-Scripting-blue?style=for-the-badge&logo=python&logoColor=white)

**Conception d'un Jumeau Numérique pour l'automatisation et la validation de réseaux critiques.**

[Voir l'Architecture](#-architecture-du-pipeline) • [Installation](#-installation--usage) • [Contacter l'auteur](#-contact)

</div>

---

## ⚠️ Note de Confidentialité
> Ce projet a été développé dans un cadre professionnel soumis à une clause de confidentialité. Le code source présent dans ce dépôt est une version **"assainie" (sanitized)** : les adresses IP réelles, les mots de passe et les topologies clients spécifiques ont été remplacés par des données génériques pour la démonstration.

---

## 📖 Le Problème & La Solution

### ❌ Le Défi
Dans les infrastructures réseaux traditionnelles, les mises à jour sont risquées. Tester une nouvelle configuration sur du matériel physique est coûteux, lent et peut impacter la production. 
**Comment valider 100% d'un changement complexe avant même de toucher au premier câble ?**

### ✅ La Solution : Le Jumeau Numérique
J'ai développé un pipeline automatisé qui :
1.  **Scanne** le réseau physique existant.
2.  **Clone** ce réseau dans un environnement virtuel (Docker/Containerlab).
3.  **Teste** les changements dans ce monde virtuel sécurisé.

**Résultat :** Réduction du temps de déploiement de plusieurs heures à **~5 minutes** et élimination des erreurs humaines.

---

## 🏗️ Architecture du Pipeline

Le système fonctionne en boucle fermée pour garantir que la simulation est toujours fidèle à la réalité.

```mermaid
graph TD
    subgraph "Monde Physique"
    A[Switches Physiques] -->|1. Scan LLDP/SNMP| B(Script Python Scanner)
    end

    subgraph "Automatisation & Données"
    B -->|2. Export Données| C{Netbox / Config}
    C -->|3. Génération YAML| D[Générateur de Topologie]
    end

    subgraph "Jumeau Numérique (Virtuel)"
    D -->|4. Déploiement| E[Containerlab + Docker]
    E -->|5. Simulation| F[Switches Virtuels (cEOS)]
    F -->|6. Validation| G[Tests Ansible & Pytest]
    end
    
    G -->|7. Feedback| H[Rapport de Validation]
