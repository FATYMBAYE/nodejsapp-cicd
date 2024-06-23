# Pipeline CI/CD pour le Projet Node.js

Ce README décrit le pipeline CI/CD mis en place pour notre projet Node.js utilisant GitHub Actions.

## Structure du Pipeline

Notre pipeline est divisé en plusieurs jobs, chacun s'exécutant dans des conditions spécifiques :

1. Analyse Semgrep

2. Job pour les branches de feature

3. Job pour les pull requests

4. Job pour les merges sur la branche principale

## Détail des Jobs

### 1. Analyse Semgrep

- S'exécute sur les événements (push et pull request sur la branche main)

- Utilise Semgrep pour l'analyse statique du code

- Génère un rapport SARIF et l'uploade pour l'analyse CodeQL de GitHub

### 2. Job pour les Branches de Feature

- S'exécute lors d'un push sur une branche commençant par "feature/"

- Teste l'application sur plusieurs versions de Node.js (16, 18, 20)

- Exécute les tests unitaires

### 3. Job pour les Pull Requests

- S'exécute lors d'une pull request vers la branche main

- Installe les dépendances

- Exécute les tests unitaires

- Lance le linter

- Effectue un scan de sécurité avec npm audit

### 4. Job pour les Merges sur Main

- S'exécute lors d'un push sur la branche main après un merge

- Exécute les tests unitaires

- Effectue un scan de sécurité

- Analyse le Dockerfile avec Hadolint

- Construit et pousse l'image Docker

- Scanne l'image Docker pour les vulnérabilités avec Trivy

## Configuration Requise

Pour que ce pipeline fonctionne correctement, on configure les secrets suivants dans le dépôt GitHub :

- DOCKER_USERNAME: Votre nom d'utilisateur Docker Hub

- DOCKER_PASSWORD: Votre mot de passe Docker Hub

## Utilisation de Matrices

Le job pour les branches de feature utilise une matrice pour tester l'application sur plusieurs versions de Node.js (16, 18, 20). Cela assure la compatibilité de l'application avec différentes versions de Node.js.

## Outils Utilisés

- Semgrep: Pour l'analyse statique du code

- npm: Pour la gestion des dépendances et l'exécution des tests

- Hadolint: Pour l'analyse du Dockerfile

- Docker: Pour la conteneurisation de l'application

- Trivy: Pour le scan des vulnérabilités de l'image Docker

## Captures d'Écran

voir le document pdf
