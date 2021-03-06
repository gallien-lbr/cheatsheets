# Mémento Docker

## Commandes utiles
```bash

# Arrêter un container
docker stop nom_container 

# Démarrer un container
docker start nom_container

# Supprime les données liées au container
docker rm  nom_container

# Affiche les conteneurs en cours d'execution
docker ps

# Affiche les conteneurs executés ou executés par le passé
docker ps -a 	

# Renommer un container
docker rename CONTAINER NEW_NAME

# Liste les images du système
docker image

# Supprimer une image
docker rmi nom_image

# Montrer l'historique d'une image
docker history [image_name]

# Montre les informations relatives à Docker du système hôte
docker info

# Relancer docker
systemctl restart docker  

# Build : construction d'une image
docker build
``` 


## Docker-compose
Docker compose permet de définir et lancer simultanément plusieurs containers (= 1 stack). 1 fichier YAML permet de de configurer les services de l'application (Redis, ElasticSearch, Php etc.).

```bash
# Lancer un stack de containers docker (flag -d = en detached [tâche de fond])
docker-compose up -d 

# Arrêter la stack de container *sans* supprimer les données
docker-compose stop

# Arrêter un stack de containers
docker-compose down

# Arrêter et supprimer les volumes
docker-compose down -v

# Arrêter un container en supprimer le volume
docker-compose rm -v NAME_CONTAINER

# Statut de la stack
docker-compose ps

# Reconstruire une image 
docker-compose build
docker-compose up --build
```

## Run basique d'une image de demo (sans paramètre ou flag)

```bash
# Crée le container et le démarre
docker run docker-whale
# par défaut se lance en mode `attached`
```

## Flags les plus utiles
```bash
-d # docker se lance en mode detached (comme un process en background)

-p host_ip:host_port:container_port #  publie le port du container (permet de publier le port en dehors de docker)

-v [repertoire_host]:[repertoire_container] # monter un volume (persistence des données, indispensable pour faire tourner une BDD avec de la persistence à l'arrêt du container (= suppression données)

-it [CONTAINER_NAME] [COMMANDE] # combo de --interactive et --tty

-e # ajoute des variables d'environnement à prendre en compte à l'exécution
```

## PostgreSQL
```bash
docker run -d -v postgres:/var/lib/postgresql/data -p 6666:5432 --name postgres -e POSTGRES_PASSWORD=root -d postgres:11
```

## Docker de stations
```bash
docker run -v C:/www/stations/src:/app -v C:/www/stations/tmp:/app/data --env-file .env -it stations  ash
```

## MariaDb
```bash
docker run -d -v mariadb:/var/lib/mysql -p 3307:3306 --name mariadb -e MYSQL_ROOT_PASSWORD=root -d mariadb:10.2
```

## Volumes (persistance des données)
### Créer un volume docker  = persister les données d'une session à une autre 
```bash
docker volume create postgres
docker volume create mariadb
```
### Lister les volumes 
```bash
docker volume ls
```

## Revenir dans un container
```bash
# Exemple sur un shell alpine=ash
docker exec -it CONTAINER_NAME ash
```

## Les images Docker
- Une image docker est l'équivalent d'un `snapshot` d'une environnement vitualisé figé. 
  Les images Docker sont immutables.

- Les images sont stockés sur les `repositories` (publics ou privés), dans un registry stocké dans le cloud.

## Les DockerFiles

Une sorte de tutoriel/descriptif de construction pour les images, qui contient toutes les commandes nécessaires à la construction d'une image. 

* Ce sont des fichiers texte simples qui contiennent toutes les instructions dont Docker a besoin pour créer une image.

* Chaque instruction du DockerFile crée un `layer`

# Références

- [OpenClassRoom - Optimisez vos déploiements avec Docker](https://openclassrooms.com/fr/courses/2035766-optimisez-votre-deploiement-en-creant-des-conteneurs-avec-docker)

- [Ref : What Is a Docker Image ?](https://searchitoperations.techtarget.com/definition/Docker-image)

- [Ref : Toutes les options de RUN](https://docs.docker.com/engine/reference/commandline/run/)
- [Ref : Références options Run](https://docs.docker.com/engine/reference/run/)
- [Ref: Tuto run](https://blog.codeship.com/the-basics-of-the-docker-run-command/)
