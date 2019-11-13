# Notes DOCKER 

## Commandes
```
docker stop nom_container 
docker start nom_container
docker rm  nom_container # supprime les données liées au container
docker ps # affiche les conteneurs en cours d'execution
docker ps -a # affiche les conteneurs executés ou executés par le passé	
docker rename CONTAINER NEW_NAME
docker image # liste les images du système
docker info
```

## Run basique d'une image de demo (sans parametre ou flag)
```
docker run docker-whale  (créer le container et le lancer)
=> par défaut se lance en mode attached
```

## Flags les plus utiles
```bash
-d : docker se lance en mode detached (comme un process en background)
-p host_ip:host_port:container_port :  publie le port du container (permet de publier le port en dehors de docker)
-v [repertoire_host]:[repertoire_container]: monter un volume (indispensable pour faire tourner une BDD avec de la persistence d'une session à l'autre)
-it [CONTAINER_NAME] [COMMANDE] => combo de --interactive et --tty
-e : ajoute des variables d'environnement à prendre en compte à l'exécution
```

- [!!!!Toutes ls options de RUN](https://docs.docker.com/engine/reference/commandline/run/)
- [Références options Run](https://docs.docker.com/engine/reference/run/)
- [Tuto run](https://blog.codeship.com/the-basics-of-the-docker-run-command/)


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

### Volumes
## Créer un volume docker pour persister les données d'une session à l'autre 
```bash
docker volume create postgres
docker volume create mariadb
```
## Lister 
```bash
docker volume ls
```

## Revenir dans un container (shell alpine=ash)
```bash
docker exec -it CONTAINER_NAME ash
```

## Les Dockerfiles

=> une sorte de tutoriel de construction pour les images. 
Ce sont des fichiers texte simples qui contiennent toutes les instructions dont Docker a besoin pour créer une image.
