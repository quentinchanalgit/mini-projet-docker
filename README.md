# mini-projet-docker
Mini-projet Easytraining

Objectifs
Les objectifs de cet examen pratique sont de garantir que vous êtes capable de gérer une infrastructure Docker.

Vous serez donc évalué sur les points suivants.

Améliorer un processus de déploiement d'applications existant
Versionner la release de l' infrastructure
Aborder les meilleures pratiques lors de la mise en œuvre de l'infrastructure Docker
Infrastructure en tant que code
Mettre en place un Registre privé


Context
POZOS est une société informatique située en France et développe des logiciels pour les lycées. Le département de l'innovation souhaite perturber l'infrastructure existante pour garantir qu'il peut être évolutif, facilement déployé avec un maximum d’automatisation.

POZOS souhaite que vous créiez un POC pour montrer comment Docker peut aider et à quel point cette technologie est efficace.

Pour ce POC, POZOS vous fournira une application et souhaite que vous construisiez une infrastructure de « découplement » basée sur Docker.

Actuellement, l'application s'exécute sur un seul serveur sans évolutivité et sans haute disponibilité.

Lorsque POZOS a besoin de déployer une nouvelle version, à chaque fois, quelque chose tourne mal.

En conclusion, POZOS a besoin d'agilité sur sa ferme logicielle.


Infrastructure
Pour ce POC, vous n’utiliserez qu’une seule machine sur laquelle Docker sera installé.

Le Build et le Déploiement se feront sur cette machine.

POZOS vous recommande d'utiliser le système d'exploitation centos7.6 car c'est le plus utilisé dans l'entreprise.


# Gestion de la Liste des Étudiants

Une application simple pour gérer une liste d'étudiants avec une API REST.

## Prérequis

- Docker et Docker Compose installés.


Prénom : Quentin

Nom : Chanal

Linkedin : https://www.linkedin.com/in/quentinchanal-alternant-ing%C3%A9nieur-cloud-devops-lyon-rhone/

Le but de ce mini-projet, était de déployer une application qui permet d'afficher la liste des étudiant avec leur age.

Dans un premier temps, je devais créer un container docker pour chaque module.


Le rôle des fichiers

Dans ma livraison, vous pouvez trouver trois fichiers principaux : un Dockerfile, un docker-compose.yml et un docker-compose.registry.yml

docker-compose.yml : pour lancer l'application (API et application web)

docker-compose.registry.yml : pour lancer le registre local et son frontend

simple_api/student_age.py : contient le code source de l'API en Python

simple_api/Dockerfile : pour construire l'image de l'API avec le code source dedans

simple_api/student_age.json : contient le nom des étudiants avec leur âge au format JSON

index.php : page PHP où l'utilisateur final sera connecté pour interagir avec le service pour lister les étudiants avec leur âge.


Build et test 

Une fois que nous avons cloné le dépot, il faut suivre les étapes pour préparer l'application student list.

cd ./mini-projet-docker/simple_api
docker build . -t api.student_age_list
docker images

Capture 

