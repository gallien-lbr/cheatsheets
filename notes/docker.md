# Notes DOCKER 

## Commandes
```
docker stop nom_container 
docker start nom_container
docker rm  nom_container
docker ps # affiche les conteneurs en cours d'execution
docker ps -a # affiche les conteneurs executés ou executés par le passé	
docker rename CONTAINER NEW_NAME
docker image # liste les images du système
```

## Run basique d'une image de demo
```
docker run docker-whale
```


## PostgreSQL
```
docker run -d -v postgres:/var/lib/postgresql/data -p 6666:5432 --name postgres -e POSTGRES_PASSWORD=root -d postgres:11
```

## Docker de stations
```
docker run -v `C:/www/stations/src:/app -v `C:/www/stations/tmp:/app/data --env-file .env -it stations  ash
```

## MariaDb
```
docker run -d -v mariadb:/var/lib/mysql -p 3307:3306 --name mariadb -e MYSQL_ROOT_PASSWORD=root -d mariadb:10.2
```


## Créer un volume docker pour persister les données d'une session à l'autre 
```
docker volume create postgres
docker volume create mariadb
```

## Revenir dans un container (shell alpine=ash)
```
docker exec -it magical_newton ash
```

## Les Dockerfiles

=> une sorte de tutoriel de construction pour les images. 
Ce sont des fichiers texte simples qui contiennent toutes les instructions dont Docker a besoin pour créer une image.
