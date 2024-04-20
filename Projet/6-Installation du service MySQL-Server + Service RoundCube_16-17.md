# 16-Installation du service MySQL-Server + Service RoundCube

```bash
apt install mysql-server -y
```

```bash
mysql -p -u root
```

```bas
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 8
Server version: 8.0.36-0ubuntu0.22.04.1 (Ubuntu)

Copyright (c) 2000, 2024, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql>

```

```bash
apt install roundcube -y
```
> 1-Yes

```bash
ln -s /usr/share/roundcube/ /var/www/html/roundcube
```
```bash
cd /usr/share/roundcube/
```
```
ls -l /var/www/html/
```
```
vi /etc/roundcube/config.inc.php
```

# 17-Tests du Webmail depuis les postes clients

Ouvrire chrome ou ...

```html
http://ns.local/roundcube/
```
> Login


![Roundcube test Karine](https://github.com/Plangloi/420-AJ5-RO_DE-PLOIEMENT-DES-SERVICES-WEB-Linux/assets/48372629/7ce73ace-eb2a-40f3-93da-dcab601c043e)



![Roundcube test Christelle](https://github.com/Plangloi/420-AJ5-RO_DE-PLOIEMENT-DES-SERVICES-WEB-Linux/assets/48372629/6093e400-4ccc-4f8c-b21a-5c2a5a7cc1e0)



