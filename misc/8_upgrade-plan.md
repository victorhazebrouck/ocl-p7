# Documentation technique – Pipeline CI/CD Orion MicroCRM

- **Auteur**: Victor Hazebrouck
- **Option choisie**: Option B (Scénario Orion)
- **Date**: 25 juin 2026

## 8. Plan de mise à jour

### 8.1 Mise à jour de l’application

#### Couvertures de test

Une couverture de tests minimale de 90% doit être atteinte et maintenue avant toute mise à jour
du système (dépendances, framework ou pipeline CI/CD). Ce seuil garantit un niveau de confiance
suffisant dans la stabilité de l’application et permet de détecter rapidement les régressions
introduites par une évolution du code. Toute mise à jour ne respectant pas ce critère doit être
bloquée dans le pipeline CI/CD jusqu’à ce que la couverture soit restaurée, afin d’assurer la
fiabilité, la maintenabilité et la sécurité continue du système.

#### Dépendances Maven / npm

Les dépendances applicatives doivent être régulièrement mises à jour afin de garantir la sécurité 
et la stabilité du projet.

- **Backend (Maven / Gradle)**:
  - Mise à jour des dépendances Spring Boot et librairies tierces
  - Utilisation de `./gradlew dependencyUpdates` ou équivalent pour identifier les versions obsolètes
  - Vérification des CVE connues via SonarQube ou OWASP Dependency Check

- **Frontend (npm)**:
  - Mise à jour via `npm update` ou outils comme `npm audit`
  - Surveillance des vulnérabilités avec `npm audit fix`
  - Éviter les versions non maintenues des packages

Objectif: réduire les vulnérabilités connues et garantir la compatibilité des composants.

#### Mises à jour Angular / Spring Boot

Les frameworks principaux doivent suivre un cycle de mise à jour contrôlé:

- **Angular**:
  - Mise à jour via `ng update`
  - Migration progressive entre versions majeures
  - Vérification des breaking changes

- **Spring Boot**:
  - Mise à jour vers versions LTS recommandées
  - Validation des changements de configuration
  - Tests de non-régression obligatoires dans le pipeline CI/CD

Une mise à jour majeure doit toujours être testée dans une branche dédiée avant merge sur `main`.

#### Mises à jour Docker (images)

Les images Docker doivent être maintenues à jour:

- Utilisation d’images de base maintenues (ex: `eclipse-temurin`, `node:lts`)
- Reconstruction régulière des images pour intégrer les patchs de sécurité
- Scan des images via outils type Trivy ou Grype
- Évitement des tags non figés (`latest` en production)

### 8.2 Mise à jour du pipeline CI/CD

#### Versions des actions GitHub

Les actions GitHub utilisées doivent être maintenues:

- `actions/checkout`
- `actions/setup-node`
- `actions/setup-java`
- `docker/build-push-action`
- `SonarSource/sonarqube-scan-action`

Bonnes pratiques:

- Fixer des versions explicites (`@v5`, `@v7`)
- Surveiller les releases des actions
- Mettre à jour progressivement pour éviter les ruptures

#### Versions des scripts

Les scripts utilisés dans le pipeline doivent être:

- Versionnés dans le dépôt Git
- Documentés et testés
- Compatibles avec les environnements CI (Ubuntu 22.04)

Exemples:

- scripts Gradle (`./gradlew`)
- scripts npm (`npm run build`, `npm run test-cov`)
- scripts Docker Compose

#### Maintenance du workflow

Le fichier `.github/workflows/ci.yml` doit être régulièrement revu:

- Suppression des étapes inutiles
- Optimisation des temps de build
- Vérification des dépendances entre jobs (`needs`)
- Ajout de nouveaux contrôles qualité (security scan, lint, etc.)

Objectif: garder un pipeline rapide, fiable et sécurisé.

### 8.3 Fréquence & bonnes pratiques

#### Conseils pour maintenir la solution dans le temps

- Effectuer des mises à jour **mensuelles minimum** des dépendances critiques
- Appliquer les correctifs de sécurité dès leur publication
- Automatiser les mises à jour mineures via Dependabot ou Renovate
- Conserver un environnement de staging pour tester les mises à jour
- Ne jamais déployer directement une mise à jour majeure en production sans validation CI complète
- Surveiller les logs CI/CD pour détecter les dégradations de performance
- Documenter chaque mise à jour importante dans le dépôt Git

Objectif global: garantir la **stabilité, la sécurité et la maintenabilité** du système dans la durée.
