# Documentation technique – Pipeline CI/CD Orion MicroCRM

- **Auteur** : Victor Hazebrouck
- **Option choisie** : Option B (Scénario Orion)
- **Date** : 25 juin 2026

## 5. Plan de sécurité

### 5.1 Résultats SonarQube (ou autre outil éventuel pour l’option A)

![sonarqube](./screenshots/sonarqube-report.png)

#### Vulnérabilités identifiées

![sonarqube](./screenshots/sonarqube-vulnerability.png)

#### Code Smells critiques

![sonarqube](./screenshots/sonarqube-code-smell.png)

<!--#### Zones de complexité-->

#### Couverture des tests

![sonarqube](./screenshots/sonarqube-coverage.png)

### 5.2 Analyse des risques

#### Vulnérabilités

L’absence des attributs integrity et crossorigin="anonymous" sur les ressources externes (scripts CDN, librairies tierces) expose l’application à des attaques de type supply chain attack.

Dans ce cas, si une dépendance externe est modifiée (compromission du CDN, injection de code malveillant, ou remplacement de fichier), le navigateur exécutera automatiquement ce code sans vérification d’intégrité.

Cela peut entraîner :

Exécution de code malveillant côté client
Vol de données utilisateurs (tokens, cookies, sessions)
Injection de scripts (XSS indirect via dépendances)
Compromission complète du front-end

Ce risque est particulièrement critique pour les applications manipulant des données sensibles (CRM, authentification, administration).

#### Risques liés au pipeline (secret mal géré, dépendance obsolète…)

Le pipeline actuel présente également plusieurs zones de risques potentiels:

- Risque si des secrets GitHub (SONAR_TOKEN, registry credentials) sont mal configurés ou exposés dans les logs
- Dépendances obsolètes
- Node.js / npm packages et dépendances Gradle peuvent contenir des vulnérabilités connues.

### 5.3 Plan d’action / Remédiation

#### Actions immédiates

Ajouter systématiquement les attributs de sécurité sur les ressources externes.
Vérifier que les secrets GitHub (SONAR_TOKEN, GITHUB_TOKEN) sont stoqués uniquement dans github secrets.

#### Actions à court terme

Mettre en place un pinning des versions des dépendances (npm / Gradle)
Ajouter un step de validation des dépendances (Dependabot ou Renovate)
Séparer clairement les environnements (staging / production) dans le job deploy
Ajouter une étape de fail-safe deployment (rollback automatique en cas d’échec)

#### Actions à long terme

Mettre en place une signature des artefacts Docker (cosign / Notary)
Automatiser la mise à jour des dépendances avec validation CI obligatoire
