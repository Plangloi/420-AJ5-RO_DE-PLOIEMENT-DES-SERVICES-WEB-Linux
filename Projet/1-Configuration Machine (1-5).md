## Configuration Serveur Ubuntu (192.168.2.10):

---

<img width="1000" alt="Ubuntu Server neofetch et ping" src="https://github.com/Plangloi/420-AJ5-RO_-Evaluation-Formative-1/assets/48372629/54c84768-80de-43d1-b219-6eccded364be">


>Ubuntu Server Neofetch et ip a


### Configuration de l' ip Statique :

#### 1- Ubuntu Server:
	
```bash
sudo nano /etc/netplan/00-installer-config.yaml
```

>Copy paste ⬇️:
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
>Attention de bien choisir l'interface Ex: enp0s5


***Configuration dans Parallels Desktop :***
<img width="500" alt="Ubuntu Parallels setup network" src="https://github.com/Plangloi/420-AJ5-RO_-Evaluation-Formative-1/assets/48372629/ee271cfe-8fe2-468b-8573-1a255ac9864a">
>Note : Mon network a la maison et dans 192.168.2.0/24 donc je peux utiliser en mode "bridge"




***SSH to Ubuntu Server :***

<img width="600" alt="ssh to ubuntu server" src="https://github.com/Plangloi/420-AJ5-RO_-Evaluation-Formative-1/assets/48372629/9566945c-6fa2-4551-89f0-8e0d94d6445f">

>ssh dans le Ubuntu server! 

```bash
ssh ipat@192.168.2.10
```
---




## Configuration Ubuntu Desktop(192.168.2.12) :

<img width="1500" alt="ubuntu Desktop neofetch" src="https://github.com/Plangloi/420-AJ5-RO_-Evaluation-Formative-1/assets/48372629/6d0e90ae-d0a7-4fba-872e-05ed2633209d">

>Unbuntu Desktop Neofetch et ip a



<img width="500" alt="Network setup in desktop" src="https://github.com/Plangloi/420-AJ5-RO_-Evaluation-Formative-1/assets/48372629/dd99b447-0cbb-45a6-a3e2-c6e1f2a3f1af">

>Network configuration dans Ubuntu Desktop



***Configuration dans Parallels Desktop :***

<img width="500" alt="Ubuntu Desktop Conf" src="https://github.com/Plangloi/420-AJ5-RO_-Evaluation-Formative-1/assets/48372629/e8d19ff7-0272-4eca-9afe-af0c0635025e">

>Note : Mon network a la maison et dans 192.168.2.0/24 donc je peux utiliser en mode "bridge"


<img width="500" alt="ssh to Unbuntu Desktop" src="https://github.com/Plangloi/420-AJ5-RO_-Evaluation-Formative-1/assets/48372629/02ffa48b-ff07-434b-aa3d-d982394ff786">

>ssh dans le Ubuntu server! 

```bash
ssh ipat@192.168.2.12
```




---
## Configuration Windows 11 (192.168.2.11):
>Windows 10 n'est pas disponible pour Arm donc jai du prendre Windows 11 🫤

<img width="1000" alt="ipconfig cmd win11" src="https://github.com/Plangloi/420-AJ5-RO_-Evaluation-Formative-1/assets/48372629/9a44b237-cf2e-4696-8450-ab45c66a51ce">


<img width="500" alt="win11 ip" src="https://github.com/Plangloi/420-AJ5-RO_-Evaluation-Formative-1/assets/48372629/96f55b68-3e01-4c8c-9794-388ca2f4089f">

>Network configuration dans Windows 11

---
## Test de connectivité :

**Unbuntu Server :**

<img width="2158" alt="Ping server" src="https://github.com/Plangloi/420-AJ5-RO_-Evaluation-Formative-1/assets/48372629/6012a086-c115-4181-b619-7b79ee57f21f">


>Ping test de Ubuntu Server a Windows 11 (192.168.2.11) et Ubuntu Desktop (192.168.2.12)

![Ping test google Ubuntu Server](https://github.com/Plangloi/420-AJ5-RO_DE-PLOIEMENT-DES-SERVICES-WEB-Linux/assets/48372629/5a114b84-3902-4c4b-a869-3430505e860d)

>Ping test to Google 8.8.8.8



**Windows 11 :**

<img width="2158" alt="win11 ping test" src="https://github.com/Plangloi/420-AJ5-RO_-Evaluation-Formative-1/assets/48372629/19f46ebb-62e7-4c63-a3d4-ca786725c4ea">


>Ping test du Windows 11 au Ubuntu Server(192.168.2.10) et Ubuntu Desktop (192.168.2.12)


![Ping google Win11](https://github.com/Plangloi/420-AJ5-RO_DE-PLOIEMENT-DES-SERVICES-WEB-Linux/assets/48372629/00a7dda7-a277-4cce-b064-2f821c2f06fe)

>Ping test to Google 8.8.8.8


**Ubuntu Desktop:**

<img width="2158" alt="ping test Ubuntu Desktop" src="https://github.com/Plangloi/420-AJ5-RO_-Evaluation-Formative-1/assets/48372629/247cc0db-3b08-4b21-8484-589f564fb080">


>Ping test du Ubuntu Desktop au Unbuntu Server (192.168.2.10) et au Pc Win11 (192.168.2.11)

![Ping google Ubuntu Desktop](https://github.com/Plangloi/420-AJ5-RO_DE-PLOIEMENT-DES-SERVICES-WEB-Linux/assets/48372629/a946b4fc-3703-4313-be0e-4e87b1b1f978)

>Ping test to Google 8.8.8.8

---
