# Documentation technique – Pipeline CI/CD Orion MicroCRM

---

## Page de titre

- **Titre du document** : Documentation technique – Industrialisation CI/CD Orion MicroCRM
- **Auteur** : Victor Hazebrouck
- **Option choisie** : Option B (Scénario Orion)
- **Date** : 25 juin 2026

---

# 1. Introduction

## Contexte du projet

L’entreprise Orion souhaite moderniser son processus de livraison logicielle afin d’automatiser les builds, les tests et les déploiements.

## Objectifs

- Automatiser le build front-end et back-end
- Automatiser les tests unitaires
- Intégrer SonarQube Cloud
- Conteneuriser l’application avec Docker
- Mettre en place un pipeline CI/CD complet

## Technologies utilisées

- Java 17 / Spring Boot / Gradle
- Node.js 20
- Docker & Docker Compose
- GitHub Actions
- SonarQube Cloud
- GitHub Container Registry

---

# 2. Pipeline CI/CD

## 2.1 Structure du pipeline

Le pipeline est déclenché sur chaque push sur la branche main.

### Étapes principales

- build-back
- build-front
- test-back
- test-front
- sonarqube
- containerization
- deploy
- dora

### Ordre d’exécution

build-back → build-front → tests → sonarqube → containerization → deploy → dora

---

## 2.2 Étapes d’automatisation

### Build back-end

```sh
./gradlew classes testClasses
```

### Build front-end

```sh
npm install
npm run build
```

### Tests back-end

```sh
./gradlew test
```

### Tests front-end

```sh
npm run test-cov
```

### Analyse SonarQube

Utilisation de :

- SonarSource/sonarqube-scan-action

---

## 2.3 Reproductibilité

### Relancer le pipeline

```sh
git add .
git commit -m "trigger pipeline"
git push origin main
```

### Gestion des secrets

- SONAR_TOKEN stocké dans GitHub Secrets
- Jamais exposé dans le code

---

# 3. Conteneurisation et déploiement

## 3.1 Dockerfiles

Principes :

- Multi-stage build
- Séparation build/runtime
- Images optimisées

---

## 3.2 Docker Compose

Services :

- front (port 80)
- back (port 8080)

### Lancement local

```sh
docker compose up --build
```

---

# 4. Plan de tests

## 4.1 Types de tests

- Tests unitaires back-end (JUnit)
- Tests front-end (Jest / Angular)
- Coverage LCOV
- Analyse qualité SonarQube

## 4.2 Exécution

- Push : tests automatiques
- Pull request : validation qualité (optionnel)
- Release : validation complète

## 4.3 Objectifs

- éviter les régressions
- garantir la qualité
- valider avant déploiement

---

# 5. Sécurité

## 5.1 SonarQube

Détection :

- vulnérabilités
- code smells
- dette technique
- complexité

## 5.2 Risques

- mauvaise gestion des secrets
- dépendances obsolètes
- absence HTTPS en local

## 5.3 Remédiation

- quality gate obligatoire
- mise à jour des dépendances
- ajout scanning sécurité

---

# 6. Monitoring & KPI

## 6.1 Métriques DORA

- Lead time
- Deployment frequency
- MTTR
- Change failure rate

## 6.2 KPI

- temps de build
- temps des tests
- taux de succès pipeline

---

# 7. Sauvegarde des données

## 7.1 Données à sauvegarder

- volumes Docker
- logs applicatifs
- artefacts CI/CD

## 7.2 Procédure de sauvegarde

- backup volumes Docker
- sauvegarde GitHub artifacts

## 7.3 Restauration

```sh
docker compose down
docker compose up -d
```

---

# 8. Mise à jour

## 8.1 Application

- dépendances Java / Node.js
- frameworks

## 8.2 CI/CD

- actions GitHub
- versions SonarQube

## 8.3 Bonnes pratiques

- mises à jour régulières
- revue pipeline

---

# 9. Conclusion

Le pipeline CI/CD permet :

- automatisation complète
- amélioration de la qualité
- réduction des erreurs
- accélération des livraisons

---

# Annexes

## Commandes utiles

```sh
./gradlew test
npm run test-cov
docker compose up
```
