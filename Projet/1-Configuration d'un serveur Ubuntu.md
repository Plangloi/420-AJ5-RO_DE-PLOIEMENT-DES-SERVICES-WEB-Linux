## Configuration Serveur Ubuntu (192.168.2.10):
![[Ubuntu Server neofetch et ping.png]]
>Ubuntu Server Neofetch et ip a
	
### Configuration de l' ip Statique :

#### 1- Ubuntu Server:
	
```bash
sudo nano /etc/netplan/00-installer-config.yaml
```

>Copy past :
```bash
#This is the network config
network:
  version: 2
  ethernets:
    enp0s5:
      addresses: [192.168.2.10/24]
      gateway4: 192.168.2.1
      dhcp4: no
      nameservers:
        addresses: [8.8.8.8]

#Pour internet:
    enp0s6:
      dhcp4: true
```

<kbd>Ctrl</kbd> + <kbd>X</kbd>
<kbd>Y</kbd>
<kbd>Enter</kbd>

***Configuration dans Parallels Desktop :***
![[/Projet/Photos/win11 ip.png]]
>Note : Mon network a la maison et dans 192.168.2.0/24 donc je peux utiliser en mode "bridge"

![[Paralllels Destop Network.png]]
>Network setup de Parallels Desktop connecté avec Host


![[ssh to ubuntu server.png]]
>ssh dans le Ubuntu server! 
>```bash
ssh ipat@192.168.2.10

---
## Configuration Ubuntu Desktop(192.168.2.12) :
![[ubuntu Desktop neofetch.png]]
>Unbuntu Desktop Neofetch et ip a
![[Network setup in desktop.png]]
>Network configuration dans Ubuntu Desktop

***Configuration dans Parallels Desktop :***
![[Ubuntu Desktop Conf.png]]
>Note : Mon network a la maison et dans 192.168.2.0/24 donc je peux utiliser en mode "bridge"


![[ssh to Unbuntu Desktop.png]]
>ssh dans le Ubuntu server! 
>```bash
ssh ipat@192.168.2.12

---
## Configuration Windows 11 (192.168.2.11):
>Windows 10 n'est pas disponible pour Arm 

![[ipconfig cmd win11.png]]

![[win11 ip.png]]
>Network configuration dans Windows 11

---
## Test de connectivité :

**Unbuntu Server :**
![[Ping server.png]]
>Ping test de Ubuntu Server a Windows 11 (192.168.2.11) et Ubuntu Desktop (192.168.2.12)

**Windows 11 :**
![[win11 ping test.png]]
>Ping test du Windows 11 au Ubuntu Server(192.168.2.10) et Ubuntu Desktop (192.168.2.12)

**Ubuntu Desktop:**
![[ping test Ubuntu Desktop.png]]
>Ping test du Ubuntu Desktop au Unbuntu Server (192.168.2.10) et au Pc Win11 (192.168.2.11)

---
