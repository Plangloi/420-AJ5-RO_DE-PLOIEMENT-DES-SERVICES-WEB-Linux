# Configuration Postfix :

```bash
sudo -s
```
```bash
apt install postfix -y
```
>type : Internet Site
>
>
>Mail name : Ubuntu

### Configuration de main.cf :

```bash
# See /usr/share/postfix/main.cf.dist for a commented, more complete version


# Debian specific:  Specifying a file name will cause the first
# line of that file to be used as the name.  The Debian default
# is /etc/mailname.
#myorigin = /etc/mailname

#New
mydomain = ns.local
home_mailbox = Maildir/
message_size_limit = 52428800

smtp_sasl_auth_enable = yes
smtp_use_tls = yes
smtp_sasl_password_maps = hash:/etc/postfix/sasl_passwd
smtp_sasl_security_options =
smtp_tls_CAfile = /etc/ssl/certs/ca-certificates.crt

mtps_sasl_auth_enable = yes

#-------

smtpd_banner = $myhostname ESMTP $mail_name (Ubuntu)
biff = no

# appending .domain is the MUA's job.
append_dot_mydomain = no

# Uncomment the next line to generate "delayed mail" warnings
#delay_warning_time = 4h

readme_directory = no

# See http://www.postfix.org/COMPATIBILITY_README.html -- default to 2 on
# fresh installs.
compatibility_level = 3.6



# TLS parameters
smtpd_tls_cert_file=/etc/ssl/certs/ssl-cert-snakeoil.pem
smtpd_tls_key_file=/etc/ssl/private/ssl-cert-snakeoil.key
smtpd_tls_security_level=may

smtp_tls_CApath=/etc/ssl/certs
smtp_tls_security_level=may
smtp_tls_session_cache_database = btree:${data_directory}/smtp_scache


smtpd_relay_restrictions = permit_mynetworks permit_sasl_authenticated defer_unauth_destination
myhostname = ubuntu.ns.local
alias_maps = hash:/etc/aliases
alias_database = hash:/etc/aliases
mydestination = $myhostname, ubuntu, ns.local , mail.ns.local , ubuntu-server, localhost.localdomain, localhost
relayhost = [smtp.gmail.com]:587
mynetworks = 127.0.0.0/8, 192.168.2.0/24
virtual_alias_maps = hash:/etc/postfix/virtual
mailbox_size_limit = 0
recipient_delimiter = +
inet_interfaces = all
inet_protocols = all
```
# Configuration du RELAIS SMTP

```bash
vi /etc/postfix/sasl_passwd
```
```bash
Ex : [smtp.gmail.com]:587 [toi]@gmail.com:[password no space]
```

## Ajouter des utilisateurs :

```bash
adduser [name]
```
- lombard
- luc
- vincent
- christelle
- arnaud
- karine
- michel

```bash
vi /etc/postfix/virtual
```
### Activer la modification avec :

```bash
postmap /etc/postfix/virtual
```
## Configurer le fichier master.cf :

```bash
vi /etc/postfix/master.cf
```
![master files](https://github.com/Plangloi/420-AJ5-RO_DE-PLOIEMENT-DES-SERVICES-WEB-Linux/assets/48372629/1b469ded-6a73-479b-b29a-353c61284c9e)

> decomanter la ligne  

```bash
systemctl restart postfix
```
### Verification que le service marche toujours :
```bash
systemctl status postfix
```
![Test status posfix](https://github.com/Plangloi/420-AJ5-RO_DE-PLOIEMENT-DES-SERVICES-WEB-Linux/assets/48372629/213d4162-4c9f-43ac-9c52-203d29213aa5)



# Test :

```bash
root@ubuntu-server:/home/ipat# mail patrice.langlois@protonmail.com
Cc:
Subject: Test de Mail Postfix

Salut Pat

    Ca marche ouiiiiiiiii!


Pat
```
> ctrl + d
>Pour Send


![Mail test](https://github.com/Plangloi/420-AJ5-RO_DE-PLOIEMENT-DES-SERVICES-WEB-Linux/assets/48372629/967904e9-0eaa-4a06-a85c-052474122f5e)





