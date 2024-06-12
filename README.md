# Fullstack with Docker

Ce dépôt contient le code source du projet Fullstack with Docker dédié à la dockerisation et au déploiement d'image docker 


Le contenu se partage en deux projets contenant chacun un Dockerfile:
- Un dossier ``backend`` proposant une API sous .NET 
- Un dossier ``frontend`` contenant une application Web basée sur celle proposée depuis le site [sandwichpouletmayonnaise.com]

Vous trouverez aussi deux fichiers `compose` pour pouvoir démarrer l'ensemble des conteneurs nécessaires

Pour comprendre le contenu de chaque projet il vous suffit de suivre les etapes 

## Installation

> Docker doit etre installer pour poursuivre l'installation []()

Pour lancer toutes les images nécessaire de la stack : 
```bash
docker compose -f docker-compose.build.yml up -d
```

Ce projet utilise comme source de données la base **mysql**. Le dump `dump.sql` contient le jeu de données pour l'application 

Pour importer les données : 
```bash
docker cp dump.sql pouletmayo-db-1:dump.sql
docker exec -it --env MYSQL_PWD=password pouletmayo-db-1 bash -c "mysql -u root -e \"CREATE DATABASE pouletmayo\""
docker exec -it --env MYSQL_PWD=password pouletmayo-db-1 bash -c "mysql -u root --default-character-set=utf8 pouletmayo < dump.sql"
# ou lancer le script
./bootstrap-mysql.sh
```

Vous aurez une API consultable en local sur le port 8000 via l'URL : http://localhost:8000.
L'API ne propose qu'un seul endpoint : [``api/entreesdujour``](http://localhost:8000/api/entreesdujour)

Un site web sera également lancé dans votre navigateur via l'adresse : http://localhost:9000 

Bonne installation et à bientôt. 
