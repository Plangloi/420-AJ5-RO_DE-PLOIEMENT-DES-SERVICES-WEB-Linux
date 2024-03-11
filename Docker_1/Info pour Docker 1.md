# 1-Site web PHP avec Docker-Compose


### Prérequis:
## Installation de :
- [ ] [Docker](https://docs.docker.com/engine/install/ubuntu/)
- [ ] [Docker-Compose](https://docs.docker.com/compose/install/)
- [ ] Connections a Internet

   
 

## Étape 1 - Création des fichiers

```
mkdir [Nouveau dossier]
```
```
cd [Nouveau dossier]
```

```
touch docker-compose.yaml index.php Dockerfile
```
```
chmod 777 docker-compose.yaml index.php Dockerfile
```
### Ajouter les commandes au fichier Dockerfile :

#
```
echo "
FROM php:8.0-apache 
RUN docker-php-ext-install mysqli && docker-php-ext-enable mysqli" > Dockerfile
```

#

### Ajouter les commandes au fichier Docker-Compose :

```
echo "

"version: '3.8'


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

" > docker-compose.yml
```
> [!CAUTION]
> Port :8010,9906,8088
> Verifier que les port son disponible!



### Ajouter les commandes au fichier index.php :

#
```
echo "
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
" > index.php

```

### Verifier si le toute est bien dans les fichier :
```
cat Docker

```
```

cat docker-compose.yml

```
```

cat index.php

```

## Démarrage des Docker avec Docker-compose :

```
sudo docker-compose up -d

```

## Stopper ou Detruire les Docker!

```
sudo docker-compose stop

```


> [!WARNING]  
> Va detruire tout les Docker!!
```
sudo docker-compose down

```



