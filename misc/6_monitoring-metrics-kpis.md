# Documentation technique – Pipeline CI/CD Orion MicroCRM

- **Auteur** : Victor Hazebrouck
- **Option choisie** : Option B (Scénario Orion)
- **Date** : 25 juin 2026

## 6. Monitoring, métriques & KPI

### 6.1 Métriques DORA

#### Lead Time

Le Lead Time observé est de **875 secondes**, correspondant au temps écoulé entre le commit et le
déploiement effectif en environnement cible. Cette valeur inclut les étapes de build, tests,
analyse qualité, conteneurisation et déploiement.

#### Deployment Frequency

Non applicable pour le moment, car les déploiements sont déclenchés principalement lors des pushs
sur la branche `main`. Une évolution vers une mesure plus fine (par environnement ou par release)
pourra être envisagée.

#### Mean Time To Restore

Non mesuré à ce stade. Cette métrique pourra être calculée lors de futurs incidents de production
en se basant sur les logs DORA et les rollback éventuels.

#### Change Failure Rate (méthode de calcul + valeurs observées)

Le Change Failure Rate est défini comme le pourcentage de déploiements ayant entraîné une erreur
nécessitant un rollback ou une correction immédiate.

```
Change Failure Rate = (Nombre de déploiements échoués / Nombre total de déploiements) × 100
```

Valeur observée :

- Non disponible actuellement (phase initiale du projet sans incidents de production significatifs)

### 6.2 KPI personnalisés

#### Temps de build

- Back: 1m 12s
- Front: 43s

#### Temps des tests

- Back: 1m 23s
- Front: 1m 01s

#### Taux d’erreurs dans les logs

- Back: 0%
- Front: 0%

### 6.3 Analyse synthétique du monitoring

#### Tendances observées

Le pipeline CI/CD montre une exécution stable avec des temps de build et de tests cohérents entre
le backend et le frontend. Le backend présente des durées légèrement plus élevées, ce qui est
attendu en raison de la compilation Java et de l’exécution des tests Spring Boot. Le frontend reste
plus rapide et plus constant. Aucun écart anormal ou dégradation progressive des performances n’a
été observé.

#### Points forts

- Pipeline entièrement automatisé et reproductible
- Bonne séparation des responsabilités entre backend et frontend
- Temps de build et de tests maîtrisés (pas de dérive excessive)
- Taux d’erreurs dans les logs à 0%, indiquant une stabilité globale
- Intégration de SonarQube pour le contrôle qualité
- Traçabilité complète via artefacts CI et logs DORA

#### Points à améliorer

- Les métriques de ci ne sont pas encore centralisées dans un outil de monitoring dédié
- Pas de corrélation automatique entre qualité de code et incidents de déploiement

#### Dashboards

TODO

#### Alertes

- Alertes SonarQube sur dépassement de Quality Gate
- Notifications GitHub Actions en cas d’échec de workflow
