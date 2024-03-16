# Wordpress avec Docker-Compose

### Prérequis:
### Avant de commencer, assurez-vous d'avoir installé Docker et Docker-Compose sur votre système.

- [ ] [Docker](https://docs.docker.com/engine/install/ubuntu/)
- [ ] [Docker-Compose](https://docs.docker.com/compose/install/)




## Étape 1 - Création des fichiers

```bash
mkdir Docker_wp && cd Docker_wp
```
```bash
touch docker-compose.yaml
```
```bash
chmod +x docker-compose.yaml
```

### Ajouter le code au fichier docker-compose.yaml :

```bash 
nano docker-compose.yaml
 ```
 Ensuite copier ceci :

```sql
version: '3.8'

services:
   db:
     image: mysql
     volumes:
       - db_data:/var/lib/mysql
     restart: always
     environment:
       MYSQL_ROOT_PASSWORD: somewordpress
       MYSQL_DATABASE: wordpress
       MYSQL_USER: wordpress
       MYSQL_PASSWORD: wordpress

   wordpress:
     depends_on:
       - db
     image: wordpress:latest
     ports:
       - "8000:80"
     restart: always
     environment:
       WORDPRESS_DB_HOST: db:3306
       WORDPRESS_DB_USER: wordpress
       WORDPRESS_DB_PASSWORD: wordpress
       WORDPRESS_DB_NAME: wordpress
volumes:
    db_data: {}
```
<kbd>Ctrl</kbd> + <kbd>X</kbd>

<kbd>Y</kbd>

<kbd>Enter</kbd>  

> [!CAUTION]
> Port : 8000

> Verifier que le port est disponible!


### Verifier si le fichier :
```bash
cat docker-compose.yaml
```

## Démarrage des Docker avec Docker-compose :
```bash
sudo docker-compose up -d
```
docker-compose up -d
```diff
Running 2/2
+Container docker_2_wp-db-1         Started
+Container docker_2_wp-wordpress-1  Started
 ```

 ## 👨🏻‍💻 Vérification!! 👨🏻‍💻

PhpMyAdmin : [localhost:8000
](http://localhost:8000)

 ![Alt text](https://github.com/Plangloi/420-AJ5-RO_-Evaluation-Formative-1/blob/main/Docker_1/Photos/Wp%20sc.png?raw=true)
#

😱 🚨 **Détruire les Docker** 🚨 😱
### Arrêtez et supprimez les conteneurs :

```bash
docker-compose down
```
docker-compose down
```diff
Running 3/3
-Container docker_2_wp-wordpress-1  Removed
-Container docker_2_wp-db-1         Removed
-Network docker_2_wp_default        Removed
```


***Q : Après avoir exécuté docker-compose up, utilisez CTRL+C suivi de docker ps -a Est-ce que les conteneurs sont stoppés ou supprimés ?***

R : Ils sont juste arrêté et non suprimés.
```bash
docker-compose up
```

> [+] Running 3/2
 ✔ Network docker_2_wp_default        Created
 ✔ Container docker_2_wp-db-1         Created
 ✔ Container docker_2_wp-wordpress-1  Created

<kbd>Ctrl</kbd> + <kbd>C</kbd>


>CGracefully stopping... (press Ctrl+C again to force)
Stopping 2/2
Container docker_2_wp-wordpress-1  ==Stopped==
Container docker_2_wp-db-1         ==Stopped==
canceled
```bash
docker ps
```
```diff
CONTAINER ID   IMAGE                             COMMAND                  CREATED        STATUS                      PORTS     NAMES
+0faa602d8b4f   wordpress:latest                  "docker-entrypoint.s…"   4 hours ago    Exited (0) 6 minutes ago              docker_2_wp-wordpress-1
+b84648d1af8a   mysql                             "docker-entrypoint.s…"   4 hours ago    Exited (0) 5 minutes ago              docker_2_wp-db-1
ef4562bbb2a6   ghcr.io/requarks/wiki:2           "docker-entrypoint.s…"   17 hours ago   Exited (0) 13 hours ago               docker_3_wiki-wiki-1
cd79f2de8550   postgres                          "docker-entrypoint.s…"   17 hours ago   Exited (0) 13 hours ago               docker_3_wiki-db-1
df8546142fa5   docker_1-php-apache-environment   "docker-php-entrypoi…"   3 days ago     Exited (0) 53 minutes ago             php-apache
4d7739ba6845   phpmyadmin/phpmyadmin             "/docker-entrypoint.…"   3 days ago     Exited (0) 10 minutes ago             docker_1-phpmyadmin-1
3358a9d5a104   mysql                             "docker-entrypoint.s…"   3 days ago     Exited (0) 10 minutes ago             db
```