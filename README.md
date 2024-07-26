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

Build et test 

Une fois que nous avons cloné le dépot, il faut suivre les étapes pour préparer l'application student list.

1. Cloner le dépôt GitHub

   git clone https://github.com/diranetafen/student-list
cd student-list


cd ./mini-projet-docker/simple_api
docker build -t api-pozos:1 .

![image](https://github.com/user-attachments/assets/8dc615b8-a826-425f-af1d-2ea698d40112)

2. Créer un réseau de type bridge pour que les deux conteneurs puissent se contacter par leurs noms grâce aux fonctions DNS.

   docker network create student_list.network --driver=bridge
docker network ls

![image](https://github.com/user-attachments/assets/5ce32682-38a2-44a1-8fac-9b6301fe00af)



3. Retourner au répertoire principal du projet, puis démarrer le conteneur de l'API backend en utilisant ces paramètres :

   
docker run --rm -d --name=api.student_age_list --network=student_list_net -v ./simple_api/:/data/ api.student_age.json -p 4000:5000 api-pozos:1 

![image](https://github.com/user-attachments/assets/152a6db0-d299-4f1f-bf3f-405688a82999)



4- Nous allons ensuite tester que l'api fonctionne avec cette commande : 

    curl -u toto:python -X GET http://127.0.0.1:4000/pozos/api/v1.0/get_student_ages  :

   

    


    




6- Démarrez le conteneur de l'application web frontale en exécutant la commande suivante :

docker run --rm -d --name=webapp.student_list -p 8082:80 --network=student_list.network -v ./website/:/var/www/html -e USERNAME=toto -e PASSWORD=python php:apache

docker ps




Infrastructure As Code

Après avoir testé  L'image API, nous allons tout assembler et déployer en utilisant docker-compose.

Docker Compose est un outil essentiel pour ce type de projet, car il permet de gérer plusieurs conteneurs de manière efficace et coordonnée. 


Le fichier docker-compose.yml déploiera deux services :

website : l'interface utilisateur finale

API : l'image construite précédemment sera utilisée avec la spécification suivante :


Pour déployer les conteneurs il faut se deplacer dans le même répertoire que notre docker-compose.yml et saisir la commande ci-dessous en mode détaché avec l'option -d


docker-compose up -d

![image](https://github.com/user-attachments/assets/6f7506d7-7c17-4996-96e6-c0a1098defbc)


docker-compose ps

![image](https://github.com/user-attachments/assets/5e109ac5-3ce5-4b10-bc5c-19eeb63bc147)





Test à partir du navigateur pour vérifier que cela fonctionne en graphique

![image](https://github.com/user-attachments/assets/6efd7915-6bde-416c-9d05-264636a24337)






Mise en place d'un registre privé

Déploiement du registre sur port 5000

Le registre sera appelé registry-pozos et sera lancé dans un réseau docker personnalisé nommé "student-list_api-pozos"

![image](https://github.com/user-attachments/assets/57796a1f-e0e0-4fb8-832e-89b7ceeeb210)

Après vérification avec la commande docker ps , le container du registre écoute bien sur le port 5000

![image](https://github.com/user-attachments/assets/2437e873-5606-4dcd-a1bd-e6527c5c66c5)

Après créé le docker registry, nous allons ensuite pousser nos images vers le registre local : 

docker tag student-list-app localhost:5000/student-list-app

docker tag : Cette commande est utilisée pour ajouter une nouvelle étiquette (tag) à une image Docker existante. L'étiquette permet d'identifier une version spécifique de l'image.

student-list-app :  nom de l'image Docker existante que vous souhaitez tagger.

localhost:5000/student-list-app :  Ici, localhost:5000 indique que l'image sera poussée vers un registre Docker local fonctionnant sur ma machine (sur le port 5000). student-list-app est le nom de l'image dans le registre.

![image](https://github.com/user-attachments/assets/ca01739f-7c36-401c-9db6-d27cb093fad5)

docker push localhost:5000/joxit/docker-registry-ui:static 

![image](https://github.com/user-attachments/assets/9acaab2a-9d57-469e-bd49-9a9e6c4d4e7c)

Cette commande envoie l'image Docker joxit/docker-registry-ui:static vers un registre Docker local hébergé sur localhost:5000. Cela permet de stocker l'image dans le registre pour une utilisation ultérieure ou pour faciliter le déploiement sur d'autres environnements.




















