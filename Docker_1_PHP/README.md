
<img src="https://www.php.net/images/php8/logo_php8_3.svg" alt="Alt text" width="150">



# Partie 1 – Site web PHP avec Docker-Compose

> ***Avant de commencer, assurez-vous d'avoir installé Docker et Docker-Compose sur votre système.***

Prérequis:

- [Docker](https://docs.docker.com/engine/install/)
- [Docker-Compose](https://docs.docker.com/compose/install/)


---



## Étape 1 - Création des fichiers

```bash
mkdir Docker_1
```
```bash
cd Docker_1
```

```bash
touch docker-compose.yaml index.php Dockerfile
```
```bash
chmod 777 docker-compose.yaml index.php Dockerfile
```






### Etape 2 - Ajouter le code au fichier Dockerfile :

```bash 
nano Dokerfile
 ```
 Ensuite copier ceci :

```bash
FROM php:8.0-apache 
RUN docker-php-ext-install mysqli && docker-php-ext-enable mysqli
```
<kbd>Ctrl</kbd> + <kbd>X</kbd>

<kbd>Y</kbd>

<kbd>Enter</kbd>

- **Ajouter le code au fichier docker-compose.yaml**

```bash 
nano docker-compose.yaml
 ```
 - ***Copier/coller ceci :***




***docker-compose.yaml***
```yaml
version: '3.8'


services:
    php-apache-environment:
      container_name: php-apache
      build:
        context: .
        dockerfile: Dockerfile
      depends_on:
        - db
      volumes:
        - .:/var/www/html/
      ports:
        - 8010:80

    db:
      container_name: db
      image: mysql
      restart: always
      environment:
        MYSQL_ROOT_PASSWORD: MYSQL_ROOT_PASSWORD
        MYSQL_DATABASE: MYSQL_DATABASE
        MYSQL_USER: MYSQL_USER
        MYSQL_PASSWORD: MYSQL_PASSWORD
      ports:
      - "9906:3306"

    phpmyadmin:
        image: phpmyadmin/phpmyadmin
        ports:
           - '8088:80'
        restart: always
        environment:
          PMA_HOST: db
        depends_on:
          - db  
```



<kbd>Ctrl</kbd> + <kbd>X</kbd>

<kbd>Y</kbd>

<kbd>Enter</kbd>  




> [!CAUTION]
> Port :8010,9906,8088

> Verifier que les port son disponible!




***Ajouter le code au fichier index.php :***
```bash
nano index.php
 ```
 - ***Copier/coller ceci :***



***index.php***
```php

<?php
$msg="";
    if(isset($_GET['reg']))
    {
     $link= mysqli_connect("db","root","MYSQL_ROOT_PASSWORD","employee");

        $qry="insert into emp_info values($_GET[txt_id],'$_GET[txt_name]','$_GET[txt_uname]','$_GET[txt_pwd]','$_GET[txt_email]',$_GET[txt_no])";

        mysqli_query($link,$qry);
        if(mysqli_affected_rows($link)>0)
        {
            $msg="<font color='green' size='5px'>Registration Done.....</font>";
        }
        else
        {
            $msg="<font color='red' size='5px'>Registration Fail.....</font>";
        }
        mysqli_close($link);
    }
?>
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title></title>
        <script>
            temp=0;
            temp1=0;
            function CheckEmail()
            {
                temp=0;
                email=document.getElementById('email').value;
                ht=new XMLHttpRequest();
                ht.open("get","Auth.php?id="+email,true);
                ht.send();
                ht.onreadystatechange=function() {
                    if(ht.readyState==4 && ht.status==200)
                    {
                        document.getElementById("d1").innerHTML=ht.responseText;
                         if(ht.responseText=="Email-Id Already Exist")
                        temp=1;
                        
                    }
                }
             
            }
            function CheckUsername()
            {
                temp1=0;
                uname=document.getElementById('uname').value;

                ht1=new XMLHttpRequest();
                ht1.open("get","Auth.php?id1="+uname,true);
                ht1.send();
                ht1.onreadystatechange=function() {
                    if(ht1.readyState==4 && ht1.status==200)
                    {
                        document.getElementById("d2").innerHTML=ht1.responseText;
                        if(document.getElementById("d2").innerHTML=="Username Already Exist")
                        {temp1=1; }
                        
                    }
                }

            }
            function validate()
            {
                if(temp==1)
               return false;
           if(temp1==1)
               return false;
           else 
               return true;
            }
        </script>
        <style>
            .mystyle{
                border-radius: 10px;
                padding-left: 5px;
                height: 25px;
                width:200px;
                font-size: 15px;
            }
            .style1{
                width:120px;
                height: 30px;
                border-radius: 10px;
                padding-left: 5px;
                font-family: Time In Roman;
                font-size: 20px;
            }
            label{
                font-family: Time In Roman;
                font-size: 20px;
            }
        </style>
    </head>
    <body>
        <hr size="4" color="green"/>
        <h2 style="font-size: 30px; color: maroon; font-family: Time In Roman; text-align: center"><br>Employee Registration Form<br></h2>
        <hr size="4" color="green"/><br>
        <div align="center"><form method="get" onsubmit="return validate()" >
                <table width="50%">
                <tr>
                    <td><label>Employee ID</label></td>
                    <td><input class="mystyle" type="text" name="txt_id" value="" required="" /></td>
                </tr>
                <tr>
                    <td><label>Employee Name</label></td>
                    <td><input class="mystyle" type="text" name="txt_name" value="" required="" /></td>
                </tr>
                <tr>
                    <td><label>Username</label></td>
                    <td><input class="mystyle" id="uname" type="text" name="txt_uname" value="" onchange="CheckUsername()" required="" /><br><div id="d2" style="color:red"></div></td>
                </tr>
                <tr>
                    <td><label>Password</label></td>
                    <td><input class="mystyle" type="password" name="txt_pwd" value="" required="" /></td>
                </tr>
                <tr>
                    <td><label>Email ID</label></td>
                    <td><input class="mystyle" id="email" type="email" name="txt_email" onchange="CheckEmail()" value="" required="" /><br><div id="d1" style="color:red"></div></td>
                </tr>
                <tr>
                    <td><label>Phone Number</label></td>
                    <td><input class="mystyle" type="text" name="txt_no" value="" required="" /></td>
                </tr>
                <tr>
                    <td></td>
                    <td><input class="style1" type="submit"  value="Register" name="reg"/></td>
                </tr>
                  <tr>
                      <td colspan="2"><?php echo $msg; ?></td>
                </tr>
            </table>
            </form></div>
    </body>
</html>
```






<kbd>Ctrl</kbd> + <kbd>X</kbd>

<kbd>Y</kbd>

<kbd>Enter</kbd>



  **Verifier le fichier :**
```bash
cat Dockerfile
```
```bash
cat docker-compose.yaml
```
```bash
cat index.php
```



### Démarrage des Docker avec Docker-compose :
```bash
sudo docker-compose up -d
```
> [+] Running 3/3
 ✔ Container db                     Running
 ✔ Container docker_1-phpmyadmin-1  Running
 ✔ Container php-apache             Running

---
###  Création de la base de données:



#### 1- Trouver le docker mysql pour accéder au bash:

```bash
docker ps
```
 Tu devrais voir quelque chose comme ça!
 ```diff
 CONTAINER ID   IMAGE                             COMMAND                  CREATED          STATUS          PORTS                               NAMES
df8546142fa5   docker_1-php-apache-environment   "docker-php-entrypoi…"   20 seconds ago   Up 19 seconds   0.0.0.0:8010->80/tcp                php-apache
4d7739ba6845   phpmyadmin/phpmyadmin             "/docker-entrypoint.…"   20 seconds ago   Up 19 seconds   0.0.0.0:8088->80/tcp                docker_1-phpmyadmin-1
+3358a9d5a104   mysql                             "docker-entrypoint.s…"   20 seconds ago   Up 19 seconds   33060/tcp, 0.0.0.0:9906->3306/tcp   db
```
Donc pour moi :

```bash
docker exec -it 3358a9d5a104 bash
```

```console
bash-4.4#
```
 > Ont devrais voir quelque chose comme ça!

Login dans base la données :

```sql
mysql -u root -p
```
>Password: MYSQL_ROOT_PASSWORD


Création de la base de données :
```sql
create database employee;
```
Vérification de la création de "employee":
```sql
show databases;
```
Utiliser la base de données "employee":
```sql
use employee;
```
Création de la table de données "emp_info" :
```sql
create table emp_info(emp_id int(11),emp_name varchar(50),emp_username varchar(50),emp_password varchar(50),emp_email varchar(50),emp_phone bigint(20)); 
```
Vérification que la table était bien Sauvegarder :
```sql
show tables;
```
```sql
desc emp_info;
```
---
## 🙀 Vérification!! 🙀

PhpMyAdmin : [localhost:8088
](http://localhost:8088)

 ![Alt text](https://github.com/Plangloi/420-AJ5-RO_-Evaluation-Formative-1/blob/main/Docker_1/Photos/phpMyAdmin.png?raw=true)


 Pages Web d'entrée de données : [localhost:8010
](http://localhost:8010)

  ![Alt text](https://github.com/Plangloi/420-AJ5-RO_-Evaluation-Formative-1/blob/main/Docker_1/Photos/data_in.png?raw=true)


User : root

Password :
```
 MYSQL_ROOT_PASSWORD
```
**Pour Stopper les docker:**  
```bash
sudo docker-compose stop
```
😱 🚨 **Détruire les Docker** 🚨 😱

```bash
sudo docker-compose down
```

