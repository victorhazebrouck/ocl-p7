# Documentation technique – Pipeline CI/CD Orion MicroCRM

- **Auteur** : Victor Hazebrouck
- **Option choisie** : Option B (Scénario Orion)
- **Date** : 25 juin 2026

## 4. Plan de testing périodique

### 4.1 Types de tests automatisés

#### Tests unitaires, d’intégration ? de sécurité (SonarQube) ?

Tests unitaires, integration, et securité.

#### Autres tests éventuels

N/A

#### quand les tests doivent être exécutés (push, merge, nightly, release…) ?

push, merge, nightly, release

#### quels tests à quelle étape ?

Tous les tests à chaque fois

#### quels critères de réussite ou d’alerte ?

Tous les tests ok -> reussite
Un test nok -> alerte

### 4.2 Fréquence d'exécution

#### Sur push

À chaque push.

#### Sur pull request

À chaque pull request.

#### Nightly build / exécution périodique

Une fois par jour.

### 4.3 Objectifs des tests

#### Qualité

Assurer la qualité du code: Correctness, Reliability, Security, Maintainability.

#### Non-régression

Assurer la non régression: Correctness, Reliability, Maintainability.

#### Vérification du bon fonctionnement avant déploiement

Assurer le bon fonctionnement du code avant de déployer.
