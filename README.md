# Documentation pour la Mise en Place d'un IXP

## Introduction

Ce document fournit des instructions détaillées pour configurer un Internet Exchange Point (IXP) en utilisant un NAS (Network Attached Storage) et un environnement de virtualisation Proxmox. L'objectif est de permettre une interconnexion efficace entre les réseaux.

## Prérequis

Avant de commencer, assurez-vous d'avoir les éléments suivants :

- Un NAS configuré pour le stockage et le partage de fichiers.
- Un serveur Proxmox installé et accessible.
- Connaissances de base en administration réseau et systèmes.

## Étapes de Configuration

### 1. Configuration du NAS

#### 1.1. Installer le logiciel NAS

- Assurez-vous que votre NAS est correctement installé et accessible via le réseau.
- Configurez les partages de fichiers nécessaires pour le stockage des données de l'IXP.

#### 1.2. Créer des utilisateurs et des permissions

- Créez des utilisateurs pour gérer l'accès au NAS.
- Définissez les permissions pour chaque utilisateur selon leurs rôles.

### 2. Configuration de Proxmox

#### 2.1. Accéder à l'interface Proxmox

- Connectez-vous à l'interface web de Proxmox à l'adresse `https://<adresse_ip_proxmox>:8006`.

#### 2.2. Configurer les interfaces réseau

1. Sélectionnez votre nœud Proxmox.
2. Allez dans l'onglet **Réseau**.
3. Créez un nouveau pont réseau (`vmbr0`) pour permettre la communication entre les VMs et l'extérieur :
   - **Nom**: `vmbr0`
   - **Ports de pont**: `eth0` (ou l'interface physique utilisée)
   - **Paramètres IPv4**: Configurez l'adresse IP si nécessaire.

#### 2.3. Créer des VMs pour l'IXP

1. Allez dans l'onglet **Création de VM**.
2. Suivez les étapes pour créer une nouvelle VM dédiée à l'IXP.
   - Assurez-vous de lui attribuer les ressources nécessaires (CPU, RAM, disque).
   - Connectez la VM au pont réseau `vmbr0`.

### 3. Configuration de l'IXP sur la VM

#### 3.1. Installer le logiciel d'IXP

- Connectez-vous à la VM via SSH ou console.
- Installez le logiciel nécessaire pour gérer l'IXP (ex. : OpenBGPd, Open vSwitch).

```bash
sudo apt update
sudo apt install openbgpd
