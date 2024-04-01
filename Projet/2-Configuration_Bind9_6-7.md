## Configuration Bind9 sur Ubuntu Server (192.168.2.10):

# Installation de Bind9
</br>

```bash
apt install bind9
```
</br>

#### Named.conf.local
```bash
nano /etc/bind/named.conf.local
```

```bash
zone "ns.local" {
                        type master;
                        file "/etc/bind/db.ns.local";
};

```
>Copy / Past ctrl+X....y....enter
</br>

#### db.ns.local
```bash
cp /etc/bind/db.local /etc/bind/db.ns.local
```

```bash
nano /etc/bind/db.ns.local
```

```bash
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     ns.local. root.ns.local. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      ns.local.
@       IN      A       192.168.2.10
dns     IN      A       192.168.2.10
pop     IN      A       192.168.2.10
pop3    IN      A       192.168.2.10
imap    IN      A       192.168.2.10
mail    IN      A       192.168.2.10
smtp    IN      A       192.168.2.10
```
>Copy / Past ctrl+X....y....enter
</br>


```bash
service bind9 restart
```
```bash
service binde status 
```
</br>

<img width="800" alt="Systemctl dind9" src="https://github.com/Plangloi/420-AJ5-RO_DE-PLOIEMENT-DES-SERVICES-WEB-Linux/assets/48372629/9a2f64ea-663d-471d-806b-bea1724299f7](https://github.com/Plangloi/420-AJ5-RO_DE-PLOIEMENT-DES-SERVICES-WEB-Linux/blob/main/Projet/Photos/Systemctl%20dind9.png">
</br>
</br>

```bash
named-checkcont /etc/bind/named.conf
```

```bash
named-checkzone ns.local /etc/bind/db.ns.local
```
</br>



#### Install resolvconf :

```bash
apt install resolvconf
```
</br>


#### Head :

```bash
nano /etc/resolvconf/resolv.conf.d/head
```
```bash
nameserver 192.168.2.10
nameserver 8.8.8.8
search ns.local
```
>Copy / Past ctrl+X....y....enter
</br>

```bash
sudo reboot
```
>login

```bash
sudo -s
```

</br>
---
</br>

### Test est vérification :
</br>


#### Unbutu Server :
</br>

#### resolv.conf :

```bash
nano /etc/resolv.conf
```

![server resolv conf](https://github.com/Plangloi/420-AJ5-RO_DE-PLOIEMENT-DES-SERVICES-WEB-Linux/assets/48372629/daf02988-a8ee-42a9-a7fd-489defa8a210)
</br>

#### Ping test :

```bash
ping ns.local
```

```bash
ping dns.ns.local
```

```bash
ping pop.ns.local
```

```bash
ping pop3.ns.local
```

```bash
ping mail.ns.local
```

```bash
ping smtp.ns.local
```
</br>
</br>
<img width="800" alt="Ping all server 2" src="https://github.com/Plangloi/420-AJ5-RO_DE-PLOIEMENT-DES-SERVICES-WEB-Linux/assets/48372629/b7f7b180-cda0-4fa9-bb1b-c3152618d726">
</br>
<img width="800" alt="Ping all from server dns pop pop3" src="https://github.com/Plangloi/420-AJ5-RO_DE-PLOIEMENT-DES-SERVICES-WEB-Linux/assets/48372629/8eac422e-307d-45c4-ba57-5efb43580710">
</br>
</br>

---
</br>

### Tests Ubuntu Destop : 

```bash
sudo -s
```
>root power
</br>
#### Hosts :
```bash
nano /etc/hosts
```

```bash
  GNU nano 6.2
127.0.0.1 localhost
127.0.1.1 ubuntu-linux-22-04-02-desktop
192.168.2.10  ns.local
# The following lines are desirable for IPv6 capable hosts
::1     ip6-localhost ip6-loopback
fe00::0 ip6-localnet
ff00::0 ip6-mcastprefix
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
```
>Copy / Past ctrl+X....y....enter

</br>
![desktop etc_hosts](https://github.com/Plangloi/420-AJ5-RO_DE-PLOIEMENT-DES-SERVICES-WEB-Linux/assets/48372629/fd0fa5ec-b6eb-40fd-961b-7a9a57fe9b56)


### Ping test :
</br>

```bash
ping ns.local
```
<img width="800" alt="Desktop Ubuntu ping nslocal" src="https://github.com/Plangloi/420-AJ5-RO_DE-PLOIEMENT-DES-SERVICES-WEB-Linux/assets/48372629/72cf6ad7-dcf5-487d-b73a-85a3ec8147b1">
</br>

### Resolv.conf :
</br>

```bash
nano /etc/resolv.conf
```

```bash
nameserver 192.168.2.10
nameserver 8.8.8.8
search ns.local
```
![desktop resov_conf](https://github.com/Plangloi/420-AJ5-RO_DE-PLOIEMENT-DES-SERVICES-WEB-Linux/assets/48372629/a76ab394-65db-4020-87ed-58511c05f137)


>Copy / Past ctrl+X....y....enter

</br>

```bash
ping smpt.ns.local
```
```bash
dig mail.ns.local
```
</br>
</br>
<img width="800" alt="Ping Desltop Ubuntu smtp" src="https://github.com/Plangloi/420-AJ5-RO_DE-PLOIEMENT-DES-SERVICES-WEB-Linux/assets/48372629/4ef3abbb-53b3-487a-97cb-0aee40249895">

![dig mail ns local](https://github.com/Plangloi/420-AJ5-RO_DE-PLOIEMENT-DES-SERVICES-WEB-Linux/assets/48372629/9686ba44-d2c3-4c75-8314-164a3951c87e)


---

## Test Windows 11


```bash
ping  ns.local
```

```bash
ping imap.ns.local
```
```bash
nslookup pop.ns.local
```

<img width="927" alt="Ping ns Windows" src="https://github.com/Plangloi/420-AJ5-RO_DE-PLOIEMENT-DES-SERVICES-WEB-Linux/assets/48372629/cbcc529f-71d7-46d3-a213-a0beab226b60">


