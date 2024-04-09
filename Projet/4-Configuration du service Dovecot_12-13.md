# Installation et Configuration du service Dovecot

```bash
apt install dovecot-pop3d -y
```

```bash
apt install dovecot-imapd -y
```
```bash
vi /etc/dovecot/dovecot.conf
```
```bash
vi /etc/dovecot/conf.d/10-mail.conf
```
```bash
vi /etc/dovecot/conf.d/10-master.conf
```
```bash
vi /etc/dovecot/conf.d/10-ssl.conf
```
```bash
vi /etc/dovecot/conf.d/10-auth.conf
```
```
cd /etc/dovecot/private/
```
```
ls
```
```
service dovecot restart
```
```
service status
```
```
systemctl status dovecot
```
# 13

```bash
echo "Test LOMBARD" | mail -s "Test Lombard CLI" lombard@ns.local
```

![Screenshot 2024-04-08 at 10 49 31 PM](https://github.com/Plangloi/420-AJ5-RO_DE-PLOIEMENT-DES-SERVICES-WEB-Linux/assets/48372629/f955fa5a-ddcb-40d3-9f51-929c135b6922)



![Screenshot 2024-04-08 at 10 54 48 PM](https://github.com/Plangloi/420-AJ5-RO_DE-PLOIEMENT-DES-SERVICES-WEB-Linux/assets/48372629/8b180cc6-e80c-4281-aa61-5b0d7408a4b2)















