<p align="center">
   <img src="./front/src/favicon.png" width="192px" />
</p>

# MicroCRM (P7 - Développeur Full-Stack - Java et Angular - Mettez en œuvre l'intégration et le déploiement continu d'une application Full-Stack)

MicroCRM est une application de démonstration basique ayant pour être objectif de servir de socle pour le module "P7 - Développeur Full-Stack".

L'application MicroCRM est une implémentation simplifiée d'un ["CRM" (Customer Relationship Management)](https://fr.wikipedia.org/wiki/Gestion_de_la_relation_client). Les fonctionnalités sont limitées à la création, édition et la visualisations des individus liés à des organisations.

![Page d'accueil](./misc/screenshots/screenshot_1.png)
![Édition de la fiche d'un individu](./misc/screenshots/screenshot_2.png)

#### Organisation

Ce [monorepo](https://en.wikipedia.org/wiki/Monorepo) contient les 2 composantes du projet "MicroCRM":

- La partie serveur (ou "backend"), en Java SpringBoot 3;
- La partie cliente (ou "frontend"), en Angular 17.


##### Dépendances

- [OpenJDK >= 17](https://openjdk.org/)
- [NPM >= 10.2.4](https://www.npmjs.com/)

#### Development:

```sh
# front
cd front
npm install
npx @angular/cli serve

# back
cd back
./gradlew build
java -jar build/libs/microcrm-0.0.1-SNAPSHOT.jar
```

#### Tests:

```sh
# front
cd front
CHROME_BIN=</path/to/google/chrome> npm test

# back
cd back
./gradlew test
```

#### Docker:

```sh
# start elk stack
docker compose -f docker-compose-elk.yml up --build

# start application
docker compose up --build
```

#### Links:

- dashboard: [http://localhost:5601](http://localhost:5601)

- front: [http://localhost](http://localhost)

- api: [http://localhost:8080](http://localhost:8080)
