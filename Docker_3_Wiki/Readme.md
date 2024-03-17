<img src="https://js.wiki/img/wikijs-full-2021.b840e376.svg" alt="Alt text" width="200">


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

 ### Vérification!

Wordpress : [localhost:3000
](http://localhost:3000)


 ![Alt text](https://github.com/Plangloi/420-AJ5-RO_-Evaluation-Formative-1/blob/main/Docker_1/Photos/wiki.png?raw=true)
> Ca marche Wiki!!!🤘🏻 

---
### 😱 🚨 **Détruire les Docker** 🚨 😱

**Arrêtez et supprimez les Docker :**

```bash
docker-compose down
```
```diff
docker-compose down

[+] Running 3/2
- ✔ Container docker_3_wiki-wiki-1  Removed
- ✔ Container docker_3_wiki-db-1    Removed
- ✔ Network docker_3_wiki_default   Removed
```
---

***Q : Vérifiez la persistance des données et les volumes pour les bases de données dans les parties précédentes***

**R : Ils sont persistance.**

```bash
docker-compose up
```
```diff
[+] Running 2/2
+ ✔ Container docker_3_wiki-db-1    Started
+ ✔ Container docker_3_wiki-wiki-1  Started
```
 ![Alt text](https://github.com/Plangloi/420-AJ5-RO_-Evaluation-Formative-1/blob/main/Docker_1/Photos/wiki%20okat%2010.22.02%20PM.png?raw=true)
> Les données sont persistance !


---
