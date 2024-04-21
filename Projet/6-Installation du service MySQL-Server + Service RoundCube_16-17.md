# 16-Installation du service MySQL-Server + Service RoundCube

```bash
apt install mysql-server -y
```

```bash
mysql -p -u root
```


Mysql login :
```
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


 installation de Rouncube sur Ubuntu Server:
```bash
apt install roundcube -y
```
1. Yes
2. Password
3. confirmation



Créer un lien vers le répertoire Roundcube :
```bash
ln -s /usr/share/roundcube/ /var/www/html/roundcube
```

Aller dans le répertoire :
```bash
cd /usr/share/roundcube/
```
```bash
ls
```
![ls usr_share_roundcude](https://github.com/Plangloi/420-AJ5-RO_DE-PLOIEMENT-DES-SERVICES-WEB-Linux/assets/48372629/041c4dc8-615e-4bd0-a51f-343a765e449f)



Lister le contenu du dossier :
```bash
ls -l /var/www/html/
```
![ls -l var](https://github.com/Plangloi/420-AJ5-RO_DE-PLOIEMENT-DES-SERVICES-WEB-Linux/assets/48372629/1e19bd51-6233-4754-85fd-b5f4d3d78380)

```bash
vi /etc/roundcube/config.inc.php
```
```php
<?php

/*
 +-----------------------------------------------------------------------+
 | Local configuration for the Roundcube Webmail installation.           |
 |                                                                       |
 | This is a sample configuration file only containing the minimum       |
 | setup required for a functional installation. Copy more options       |
 | from defaults.inc.php to this file to override the defaults.          |
 |                                                                       |
 | This file is part of the Roundcube Webmail client                     |
 | Copyright (C) The Roundcube Dev Team                                  |
 |                                                                       |
 | Licensed under the GNU General Public License version 3 or            |
 | any later version with exceptions for skins & plugins.                |
 | See the README file for a full license statement.                     |
 +-----------------------------------------------------------------------+
*/

$config = array();
////////////////////// $config = [];

// Do not set db_dsnw here, use dpkg-reconfigure roundcube-core to configure database!
include_once("/etc/roundcube/debian-db-roundcube.php");

// The IMAP host chosen to perform the log-in.
// Leave blank to show a textbox at login, give a list of hosts
// to display a pulldown menu or set one host as string.
// Enter hostname with prefix ssl:// to use Implicit TLS, or use
// prefix tls:// to use STARTTLS.
// Supported replacement variables:
// %n - hostname ($_SERVER['SERVER_NAME'])
// %t - hostname without the first part
// %d - domain (http hostname $_SERVER['HTTP_HOST'] without the first part)
// %s - domain name after the '@' from e-mail address provided at login screen
// For example %n = mail.domain.tld, %t = domain.tld
$config['default_host'] = 'ns.local';

// SMTP server host (for sending mails).
// Enter hostname with prefix ssl:// to use Implicit TLS, or use
// prefix tls:// to use STARTTLS.
// Supported replacement variables:
// %h - user's IMAP hostname
// %n - hostname ($_SERVER['SERVER_NAME'])
// %t - hostname without the first part
// %d - domain (http hostname $_SERVER['HTTP_HOST'] without the first part)
// %z - IMAP domain (IMAP hostname without the first part)
// For example %n = mail.domain.tld, %t = domain.tld
// To specify different SMTP servers for different IMAP hosts provide an array
// of IMAP host (no prefix or port) and SMTP server e.g. ['imap.example.com' => 'smtp.example.net']
$config['smtp_server'] = 'ns.local';

// SMTP port. Use 25 for cleartext, 465 for Implicit TLS, or 587 for STARTTLS (default)
$config['smtp_port'] = 587;

// SMTP username (if required) if you use %u as the username Roundcube
// will use the current username for login
$config['smtp_user'] = '';

// SMTP password (if required) if you use %p as the password Roundcube
// will use the current user's password for login
$config['smtp_pass'] = '%p';

// provide an URL where a user can get support for this Roundcube installation
// PLEASE DO NOT LINK TO THE ROUNDCUBE.NET WEBSITE HERE!
$config['support_url'] = '';

// Name your service. This is displayed on the login screen and in the window title
$config['product_name'] = 'Roundcube Webmail';

// This key is used to encrypt the users imap password which is stored
// in the session record. For the default cipher method it must be
// exactly 24 characters long.
// YOUR KEY MUST BE DIFFERENT THAN THE SAMPLE VALUE FOR SECURITY REASONS
$config['des_key'] = 'ciYdH+iI8Tky1CflrtMg7nkK';

// List of active plugins (in plugins/ directory)
// Debian: install roundcube-plugins first to have any
$config['plugins'] = [
    // 'archive',
    // 'zipdownload',
];

// skin name: folder from skins/
$config['skin'] = 'elastic';

// Disable spellchecking
// Debian: spellchecking needs additional packages to be installed, or calling external APIs
//         see defaults.inc.php for additional informations
$config['enable_spellcheck'] = false;
```

# 17-Tests du Webmail depuis les postes clients
## Windows 11 :
1. Ouvrire chrome ou.....
2. [http://ns.local/roundcube](http://ns.local/roundcube)
3. Login : karine
4. pasword: XXXX
5. Evoyer email @ lombard@ns.local


Verification de reception de email de Karine dans Thunderbird dans Windows 11 :
![Roundcube test Karine](https://github.com/Plangloi/420-AJ5-RO_DE-PLOIEMENT-DES-SERVICES-WEB-Linux/assets/48372629/7ce73ace-eb2a-40f3-93da-dcab601c043e)

1. Ouvrire chrome ou.....
2. [http://ns.local/roundcube](http://ns.local/roundcube)
3. Login : Christelle
4. pasword: XXXX
5. Evoyer email @ arnaud@ns.local

Verification de reception de email de Christelle dans Thunderbird dans Ubuntu Desktop :
![Roundcube test Christelle](https://github.com/Plangloi/420-AJ5-RO_DE-PLOIEMENT-DES-SERVICES-WEB-Linux/assets/48372629/6093e400-4ccc-4f8c-b21a-5c2a5a7cc1e0)

Fin

# Merci

