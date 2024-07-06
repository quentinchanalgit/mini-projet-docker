# mini-projet-docker
Mini-projet Easytraining


L'objectif de cet examen pratique est de garantir la gestion d'une infrastructure Docker.

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
Pour ce POC, nous n'aurons besoin que d'une seule machine sur laquelle Docker sera installé.

Le Build et le Déploiement se feront sur cette machine.

POZOS recommande d'utiliser le système d'exploitation centos7.6 car c'est le plus utilisé dans l'entreprise.


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

1.

cd ./mini-projet-docker/simple_api
docker build . -t api.student_age_list
docker image

Capture 

2. Créer un réseau de type bridge pour que les deux conteneurs puissent se contacter par leurs noms grâce aux fonctions DNS.

   docker network create student_list.network --driver=bridge
docker network ls

Capture 


3. Retourner au répertoire principal du projet, puis démarrer le conteneur de l'API backend en utilisant ces paramètres :

   cd ..
docker run --rm -d --name=api.student_age_list --network=student_list_net -v ./simple_api/:/data/ api.student_age
docker ps

Capture


4- Avant de démarrer le conteneur du site web, nous allons mettre à jour la ligne suivante dans le fichier index.php, afin que api_ip_or_name et port correspondent à notre configuration :

    -i s\<api_ip_or_name:port>\api.student_list:5000\g ./website/index.php

    Capture


5- Le nom d'utilisateur et le mot de passe sont fournis dans le code source.

.simple_api/student_age.py

Capture


6- Démarrez le conteneur de l'application web frontale en exécutant la commande suivante :

docker run --rm -d --name=webapp.student_list -p 8082:80 --network=student_list.network -v ./website/:/var/www/html -e USERNAME=toto -e PASSWORD=python php:apache
docker ps


Capture

7- Test de l'API via le frontend 

Capture


Pour finir, nous nettoyons l'espace de travail : 

docker stop api.student_list
docker stop webapp.student_list
docker network rm student_list.network
docker network ls
docker ps

Capture 








