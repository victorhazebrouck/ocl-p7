# Documentation technique – Pipeline CI/CD Orion MicroCRM

- **Auteur**: Victor Hazebrouck
- **Option choisie**: Option B (Scénario Orion)
- **Date**: 25 juin 2026

## 7. Plan de sauvegarde des données

### 7.1 Ce qui doit être sauvegardé

#### Fichiers de configuration

Les éléments critiques à sauvegarder incluent:

- Fichiers de configuration applicative:
  - `application.yml` / `application.properties` (backend Spring Boot)
  - Variables d’environnement (non commitées)
- Fichiers de configuration CI/CD:
  - `.github/workflows/ci.yml`
- Configuration Docker:
  - `docker-compose.yml`
  - `Dockerfile` (front et back)
- Scripts de déploiement et d’initialisation

Ces éléments permettent de reconstruire entièrement l’environnement applicatif en cas de perte.

#### Artefacts de build

Les artefacts générés dans le pipeline doivent également être sauvegardés:

- Rapports de tests backend:
  - `back/build/reports/`
- Rapports de couverture frontend:
  - `front/coverage/`
- Résultats SonarQube (Quality Gate, analyses)
- Images Docker générées et publiées:
  - stockées dans GitHub Container Registry (GHCR)

Ces artefacts permettent de:

- restaurer une version stable
- analyser un incident passé
- reproduire un build exact

### 7.2 Procédure de sauvegarde

#### Format

Les sauvegardes sont effectuées sous plusieurs formats:

- Artefacts CI/CD: fichiers ZIP gérés par GitHub Actions (`upload-artifact`)
- Images Docker: stockées dans GHCR (`ghcr.io`)
- Logs et rapports: fichiers NDJSON / HTML / XML selon les outils
- Code source: versionné via Git (GitHub)

#### Fréquence

- À chaque push sur `main`: génération des artefacts et images Docker
- À chaque pull request: exécution des tests et génération des rapports
- Tous les jours à 02h00 (UTC): exécution du pipeline via `schedule` (build + tests + analyse)
- Sauvegarde continue implicite via Git (chaque commit est historisé)

#### Outils utilisés

- GitHub Actions: orchestration CI/CD et stockage d’artefacts
- GitHub (Git): versioning du code source
- GitHub Container Registry (GHCR): stockage des images Docker
- `actions/upload-artifact`: sauvegarde des rapports de test
- SonarQube: analyse qualité du code
- Docker: packaging des applications

### 7.3 Procédure de restauration

#### Scénario d’incident

Les scénarios suivants sont pris en compte:

- Déploiement d’une version instable en production
- Régression fonctionnelle après merge sur `main`
- Image Docker corrompue ou vulnérable
- Perte de disponibilité du service après release

#### Étapes pour revenir à une version stable

**1. Identifier une version fiable**

- Consulter l’historique Git (`git log`)
- Identifier un commit stable validé par:
  - SonarQube Quality Gate OK
  - tests réussis
  - déploiement réussi (DORA log)

**2. Restaurer le code**

```bash
git checkout <commit-id-stable>
# or
git revert <commit-id-problématique>
git push origin main
```

**3. Restaurer le deployement**

- Géré automatiquement par la pipeline.
