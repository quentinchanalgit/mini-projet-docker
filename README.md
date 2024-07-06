# mini-projet-docker
Mini-projet Easytraining

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


