# Documentation technique – Pipeline CI/CD Orion MicroCRM

- **Auteur** : Victor Hazebrouck
- **Option choisie** : Option B (Scénario Orion)
- **Date** : 25 juin 2026

## 1. Introduction

### Contexte du projet

L’entreprise Orion souhaite moderniser son processus de livraison logicielle afin d’automatiser les builds, les tests et les déploiements.

### Objectifs de l’industrialisation

- Automatiser le build front-end et back-end
- Automatiser les tests unitaires
- Intégrer SonarQube Cloud
- Conteneuriser l’application avec Docker
- Mettre en place un pipeline CI/CD complet

### Technologies principales

- Java 17 / Spring Boot / Gradle
- Node.js 20
- Docker & Docker Compose
- SonarQube Cloud
- GitHub Actions
- GitHub Container Registry

### Présentation rapide du pipeline CI/CD mis en place

- build-back
- build-front
- test-back
- test-front
- sonarqube
- containerization
- deploy
- dora
