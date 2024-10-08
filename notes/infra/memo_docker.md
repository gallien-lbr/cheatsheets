# Mémento Docker

**Docker:** outil de "containerisation". Permet de standardiser les composants logiciels et de les déployer plus facilement par la suite, dans une approche "DevOPS" (ex: sur un orchestrateur tel que K8S ou Docker Swarm)

**v1 publique sortie en 2013.**

## Architecture / Terminologie

* **Moteur Docker Engine ou Docker Daemon** = exécuté en mode service
* **Docker client** = connexion au serveur docker
* **Image** = Contiennent les applications à exécuter (toujours en lecture seule / stocké en local / distribué par registry ou construit par le dév)
* **Container** = instance de l'image en cours d'exécution
* **Registry** = Distribution des librairies d'images  (par défaut : hub.docker.com ou self-hosté : exemple Harbor)

## Bonnes pratiques 

### Images Dockers
La logique à mettre en place doit être axée sur l'optimisation des images. 
Images doivent être portables, rapides, donc les plus petites possibles.
Moins on expose de fonctionnalités au sein de l'image , plus le spectre de vulnérabilités est faible. (outil de vérification des CVE : `trivy`)

### Execution
Par défaut le socket Docker est exécuté en root, et mutualise les ressources pour l'ensembles des containers. 
Il ne faut pas partir sur une setup docker "natif" en production, sans faire au préalable de configuration de sécurité custom.

### Fichier entrypoint-point.sh

`entrypoint.sh` fichier utilisé pour lancer des commandes à l'exécution du container (remplace le CMD à rallonge dans le dockerfile).
Par défaut le container se démarre et s'éteint. Il n'a pas d'état. Cela permet de lancer des services (service apache, php, mysql etc.) 
donne de la flexibilité car exite de devoir remodifier et build l'image, mais présente une faille de sécurité car permet de modifier l'image.
A utiliser pour du dév.

## Set des variables d'environnements

- The .env file in the project root, and the env_file: field in the Compose file are two different concepts.
- The **.env** is for settings a default environment for Compose. Values set in this file can be used within the Compose file.
- The **env_file**: field is for setting the default environment for a container. Values set in this can be used in the container, but not in the Compose file.


## Commandes utiles
```bash
# Voir si docker tourne
ps aux | grep docker

# Retrouver les "layers" d'une image (version "buildé")
docker history [image:tag]

# Inspecter / Obtenir des infos sur un container
docker inspect [...]

# Arrêter un container
docker stop [nom_container] 

# Démarrer un container
docker start [nom_container]

# Supprime les données liées au container
docker rm  [nom_container]

# Affiche les conteneurs en cours d'execution
docker ps

# Affiche les conteneurs executés ou executés par le passé
docker ps -a 	

# Renommer un container
docker rename [CONTAINER NEW_NAME]

# Liste les images du système
docker images

# Supprimer une image
docker rmi nom_image
docker rm -f nom_image

# Montre les informations relatives à Docker du système hôte
docker info

# Lancer/Relancer le daemon docker
sudo systemctl [start/restart] docker

# Build : construction d'une image
docker build
``` 


## Docker exécution d'un container à partir d'une image

```bash
docker run --name njs node:10.18.0-stretch-slim
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

# Lancer les services docker-compose avec un mode verbeux
docker-compose --verbose  up -d

# Récupérer les logs
 docker-compose logs
```


## Run basique d'une image avec Docker run (sans paramètre ou flag)

```bash
# Crée le container et le démarre
docker run docker-whale
# par défaut se lance en mode `attached`
```

### Exemple run d'une image PostgreSQL
```bash
docker run -d -v postgres:/var/lib/postgresql/data -p 6666:5432 --name postgres -e POSTGRES_PASSWORD=root -d postgres:11
```

### Exemple run d'une image Docker applicative
```bash
docker run -v C:/www/stations/src:/app -v C:/www/stations/tmp:/app/data --env-file .env -it stations  ash
```

### Exemple run d'une image MariaDb
```bash
docker run -d -v mariadb:/var/lib/mysql -p 3307:3306 --name mariadb -e MYSQL_ROOT_PASSWORD=root -d mariadb:10.2
```

## Flags les plus utiles
```bash
-d # docker se lance en mode detached (comme un process en background)

-p host_ip:host_port:container_port #  publie le port du container (permet de publier le port en dehors de docker)

-v [repertoire_host]:[repertoire_container] # monter un volume (persistence des données, indispensable pour faire tourner une BDD avec de la persistence à l'arrêt du container (= suppression données)

-it [CONTAINER_NAME] [COMMANDE] # combo de --interactive et --tty

-e # ajoute des variables d'environnement à prendre en compte à l'exécution
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

**Objectif : Automatiser la création d'image**

Une sorte de tutoriel/descriptif de construction pour les images, qui contient toutes les commandes nécessaires à la construction d'une image. 

* Ce sont des fichiers texte simples qui contiennent toutes les instructions dont Docker a besoin pour créer une image.

* Chaque instruction du DockerFile crée un `layer` => les layers sont mis en cache au moment du build et ne sont pas rejoué (sans si invalidation du cache spécifié en option)

* La déclaration d'un DockerFile doit commencer par l'instruction **"FROM"**, qui spécifie l'image parent.

### Multi-stage build
Bonne pratique pour séparer dans une image ce qui va être exécuté (en run du container) de ce qui va être build au moment de la création de l'image. 
L'objectif est d'éliminer le superflu ou ce qui pourrait poser problème en terme de sécurité (ex : outils de compilation) 

### Récupération d'une image au sein d'un Dockerfile 
Exemple: on récupére l'image Docker de composer ici : 
```docker
COPY --from=composer:2 /usr/bin/composer /usr/bin/composer
```

### Docker outils 
- [Busybox - outils linux utiles pour debug](https://www.busybox.net/)
- [Gron - make json greppable](https://github.com/tomnomnom/gron)
- [image Alpine - linux de base en 5mb](https://hub.docker.com/_/alpine)
- [nix os - nixery](https://nixos.org)

# Références

- [OpenClassRoom - Optimisez vos déploiements avec Docker](https://openclassrooms.com/fr/courses/2035766-optimisez-votre-deploiement-en-creant-des-conteneurs-avec-docker)
- [Ref : What Is a Docker Image ?](https://searchitoperations.techtarget.com/definition/Docker-image)
- [Ref : Toutes les options de RUN](https://docs.docker.com/engine/reference/commandline/run/)
- [Ref : Références options Run](https://docs.docker.com/engine/reference/run/)
- [Ref: Tuto run](https://blog.codeship.com/the-basics-of-the-docker-run-command/)
- [Simple docker setup for symfony](https://medium.com/accesto/simple-docker-setup-for-symfony-project-accesto-blog-9dc4e3179642)
- [Step debbuging in xdebug 3](https://matthewsetter.com/setup-step-debugging-php-xdebug3-docker/)
- [XDEBUG PHP DOCKER SF](https://www.pascallandau.com/blog/phpstorm-docker-xdebug-3-php-8-1-in-2022/#install-xdebug) 
