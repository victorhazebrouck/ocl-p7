# Documentation technique – Pipeline CI/CD Orion MicroCRM

- **Auteur** : Victor Hazebrouck
- **Option choisie** : Option B (Scénario Orion)
- **Date** : 25 juin 2026

## 2. Étapes de mise en œuvre du pipeline CI/CD

### 2.1 Structure du pipeline

Le pipeline est déclenché sur chaque push sur la branche main.

#### Étapes principales

- build-back
- build-front
- test-back
- test-front
- sonarqube
- containerization
- deploy
- dora

#### Ordre d’exécution

```
build-back  → test-back
                         → sonarqube → containerization → deploy → dora
build-front → test-front
```

#### Justification du choix des actions GitHub

- actions/checkout@v5
- gradle/actions/setup-gradle@v5
- actions/setup-java@v5
- actions/setup-node@v6
- actions/upload-artifact@v6
- actions/checkout@v6
- actions/download-artifact@v8.0.1
- SonarSource/sonarqube-scan-action@v7.1.0
- docker/login-action@v4
- docker/metadata-action@v6
- docker/build-push-action@v7

### 2.2 Scripts d’automatisation

#### Scripts utilisés

N/A

#### Leur rôle dans le pipeline

N/A

#### Comment les exécuter ou les adapter

N/A

### 2.3 Reproductibilité

#### Comment relancer le pipeline

Push ou relancer sur github directement.

#### Gestion des secrets (sans jamais les afficher)

- `SONAR_TOKEN`: à aller chercher sur sonarqube cloud et renseigner sur le depot github.
