# Configuration des boites mails avec Thunderbird :


```bash
vi /etc/postfix/main.cf
```
```yml
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

#smtps_sasl_auth_enable = yes

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

```bash
service posfix restart
```

## Windows 11 email configuration :

![Mail setup Windows ](https://github.com/Plangloi/420-AJ5-RO_DE-PLOIEMENT-DES-SERVICES-WEB-Linux/assets/48372629/a54824f7-84a2-4ae0-8407-8762d9801a20)

>Windows Setup avec Thunderbird (Marche mieux)

## Ubuntu Destop email Configuration  :

![Mail setup ubuntu Desktop](https://github.com/Plangloi/420-AJ5-RO_DE-PLOIEMENT-DES-SERVICES-WEB-Linux/assets/48372629/bed562b5-e326-4695-a19a-bd35218eaf20)

>Ubuntu Destop setup avec Thunderbird


# Tests des boites mails avec Courrier et Thunderbird :

![Mail Test ok](https://github.com/Plangloi/420-AJ5-RO_DE-PLOIEMENT-DES-SERVICES-WEB-Linux/assets/48372629/6f4a2cc3-6851-4de2-a107-1b67ab147024)
