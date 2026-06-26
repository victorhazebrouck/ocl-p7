# Documentation technique – Pipeline CI/CD Orion MicroCRM

- **Auteur** : Victor Hazebrouck
- **Option choisie** : Option B (Scénario Orion)
- **Date** : 25 juin 2026

## 9. Conclusion

#### Résumé des améliorations apportées

La mise en place du pipeline CI/CD Orion MicroCRM a permis d’automatiser l’ensemble du cycle de vie
applicatif, depuis la compilation jusqu’au déploiement. Le projet intègre désormais des étapes de
build séparées pour le front et le back, des phases de tests automatisés, ainsi qu’une analyse de
qualité de code via SonarQube. La conteneurisation des applications et la publication des images
Docker dans le GitHub Container Registry assurent une distribution standardisée et reproductible.
Enfin, l’ajout d’un reporting DORA permet de suivre les performances du cycle de livraison.

#### Gains observés (fiabilité, rapidité, qualité)

L’automatisation du pipeline a significativement amélioré la fiabilité des livraisons en réduisant
les erreurs humaines lors des déploiements. La séparation des jobs et l’exécution parallèle des
étapes de build et de test ont permis d’optimiser les temps d’exécution globaux. La qualité du code
est désormais mieux contrôlée grâce à SonarQube et aux rapports de tests automatisés. En parallèle,
la traçabilité des versions et des déploiements est renforcée grâce aux artefacts CI/CD et aux
images Docker versionnées.

#### Recommandations pour les itérations suivantes

Pour les futures évolutions du projet, il est recommandé de renforcer encore la sécurité du
pipeline en ajoutant des scans de vulnérabilités sur les images Docker et les dépendances
applicatives. La mise en place de quality gates bloquants sur SonarQube permettrait d’empêcher tout
déploiement en cas de régression critique. Il serait également pertinent d’introduire un
environnement de staging distinct pour valider les déploiements avant production. Enfin,
l’intégration de mécanismes de rollback automatisé et de signature des artefacts améliorerait
encore la robustesse globale de la chaîne CI/CD.
