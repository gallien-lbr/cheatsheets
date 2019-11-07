# docker
```
docker run -d -v postgres:/var/lib/postgresql/data -p 6666:5432 --name postgres -e POSTGRES_PASSWORD=root -d postgres:11
docker stop nom_container 
docker start nom_container
docker rm  nom_container
docker ps
```
```
## lancer le docker de stations
docker run -v `C:/www/stations/src:/app -v `C:/www/stations/tmp:/app/data --env-file .env -it stations  ash

## creer un volume docker pour persister les données d'une session à l'autre 
docker volume create postgres

## revenir dans une VM (shell alpine=ash)
docker exec -it magical_newton ash

## mariadb
docker run -d -v mariadb:/var/lib/mysql -p 3307:3306 --name mariadb -e MYSQL_ROOT_PASSWORD=root -d mariadb:10.2
```