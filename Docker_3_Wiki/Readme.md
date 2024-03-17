#  Wiki.js avec Docker-Compose

> ***Avant de commencer, assurez-vous d'avoir installé Docker et Docker-Compose sur votre système.***

Prérequis:

- [Docker](https://docs.docker.com/engine/install/)
- [Docker-Compose](https://docs.docker.com/compose/install/)


---

### Étape 1 - Création des fichiers :

```bash
mkdir Docker_wiki && cd Docker_wiki
```
```bash
touch docker-compose.yaml
```
```bash
chmod +x docker-compose.yaml
```


- **Ajouter le code au fichier docker-compose.yaml**

```bash 
nano docker-compose.yaml
 ```
 - ***Copier/coller ceci :***
 ***docker-compose.yaml***

```sql
version: "3.8"
services:

  db:
    image: postgres
    environment:
      POSTGRES_DB: wiki
      POSTGRES_PASSWORD: wikijsrocks
      POSTGRES_USER: wikijs
    logging:
      driver: "none"
    restart: unless-stopped
    volumes:
      - db-data:/var/lib/postgresql/data

  wiki:
    image: ghcr.io/requarks/wiki:2
    depends_on:
      - db
    environment:
      DB_TYPE: postgres
      DB_HOST: db
      DB_PORT: 5432
      DB_USER: wikijs
      DB_PASS: wikijsrocks
      DB_NAME: wiki
    restart: unless-stopped
    ports:
      - "3000:3000"

volumes:
  db-data:
```
<kbd>Ctrl</kbd> + <kbd>X</kbd>

<kbd>Y</kbd>

<kbd>Enter</kbd>  

> [!CAUTION]
> Port : 3000

  **Verifier le fichier ***docker-compose***.yaml :**
```bash
cat docker-compose.yaml
```

---


### Étape 2 - Démarrage des Docker avec Docker-compose :
```bash
sudo docker-compose up -d
```
```diff
[+] Running 2/2
+ ✔ Container docker_3_wiki-db-1    Started
+ ✔ Container docker_3_wiki-wiki-1  Started
 ```

 ---

 ### Vérification!

Wordpress : [localhost:3000
](http://localhost:3000)


 ![Alt text](https://github.com/Plangloi/420-AJ5-RO_-Evaluation-Formative-1/blob/main/Docker_1/Photos/Wp%20sc.png?raw=true)
> Ca marche!!!🤘🏻 

---
### 😱 🚨 **Détruire les Docker** 🚨 😱

**Arrêtez et supprimez les Docker :**

```bash
docker-compose down
```
```diff
Running 3/3
-Container docker_2_wp-wordpress-1  Removed
-Container docker_2_wp-db-1         Removed
-Network docker_2_wp_default        Removed
```
---

***Q : Après avoir exécuté docker-compose up, utilisez CTRL+C suivi de docker ps -a Est-ce que les conteneurs sont stoppés ou supprimés ?***

**R : Ils sont juste arrêté et non suprimés.**
```bash
docker-compose up
```
```diff
[+] Running 3/2
+ ✔ Network docker_2_wp_default        Created
+ ✔ Container docker_2_wp-db-1         Created
+ ✔ Container docker_2_wp-wordpress-1  Created
```
<kbd>Ctrl</kbd> + <kbd>C</kbd>

```diff
Gracefully stopping... (press Ctrl+C again to force)
Stopping 2/2
-Container docker_2_wp-wordpress-1  Stopped
-Container docker_2_wp-db-1         Stopped
canceled
```
```bash
docker ps -a
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
---
