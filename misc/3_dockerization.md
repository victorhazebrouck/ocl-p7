# Documentation technique – Pipeline CI/CD Orion MicroCRM

- **Auteur** : Victor Hazebrouck
- **Option choisie** : Option B (Scénario Orion)
- **Date** : 25 juin 2026

## 3. Plan de conteneurisation et de déploiement

### 3.1 Dockerfiles

#### Principaux choix techniques

- FROM node AS front-build
- FROM gradle:jdk17 AS back-build
- FROM alpine:3.19 AS front
- FROM alpine:3.19 AS back
- FROM alpine:3.19 AS standalone

#### Explication du multi-stage build

### 3.2 docker-compose.yml

#### Services définis

##### application

- front
- back

##### elk

- elasticsearch
- kibana
- logstash

#### Instructions pour lancer l’application localement

```sh
# start elk stack
docker compose -f docker-compose-elk.yml up --build

# start application
docker compose up --build
```

- dashboard: [http://localhost:5601](http://localhost:5601)
- front: [http://localhost](http://localhost)
- api: [http://localhost:8080](http://localhost:8080)
