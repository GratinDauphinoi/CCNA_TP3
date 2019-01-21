# I. Création et utilisation simples d'une VM CentOS

## 1. Création

## 2. Installation de l'OS

## 3. Premier boot

## 5. Faire joujou avec quelques commandes

#### Ping
Hote ---> VM

![](https://github.com/GratinDauphinoi/CCNA_TP3/blob/master/1.png?raw=true)

VM ---> Hote

![](https://github.com/GratinDauphinoi/CCNA_TP3/blob/master/2.png?raw=true)

#### Afficher la table de routage 

de l'hote

![](https://github.com/GratinDauphinoi/CCNA_TP3/blob/master/Table%20de%20routage%20hote.png?raw=true)

de la VM

![](https://github.com/GratinDauphinoi/CCNA_TP3/blob/master/Table%20routage%20VM.png?raw=true)

#### Depuis la VM utilisez curl (ou wget) pour télécharger un fichier sur internet

![](https://github.com/GratinDauphinoi/CCNA_TP3/blob/master/Curl.png?raw=true)

# II. Notion de ports et SSH

## 1. Exploration des ports locaux
Utilisez la commande ```ss```pour lister les ports TCP sur lesquels la machine virtuelle écoute.
pour avoir uniquement les connexions en IPv4, on peut utiliser ```ss -4```


![](https://github.com/GratinDauphinoi/CCNA_TP3/blob/master/ss%20-4.PNG?raw=true)

## 2. SSH

Après création d'un serveur SSH sur la VM, nous nous connectons via "putty"

![](https://github.com/GratinDauphinoi/CCNA_TP3/blob/master/putty.PNG?raw=true)

## 3. Firewall

#### A. SSH :
La connexion échoue car le firewall bloque tous les ports qui n'ont pas d'exceptions 

Il faut donc ouvrir le port 2222
```bash
firewall-cmd --add-port=2222/tcp --permanent
```
De la on peut se reconnecter a Putty.

#### B. Netcat
On ouvre le port 5454 :
```bash
firewall-cmd --add-port=5454/tcp --permanent
```
On lance netcat sur la vm :
```bash
nc -l 5454
```
Sur windows on communique avec la VM:
```bash
.\nc
Cmd line: 192.168.127.10 5454
Alo la Vm
Oui Windows
```
On visualise la connexion netcat en cours
```bash
netstat -n
  TCP    192.168.:1137     192.168.102.1:5454    ESTABLISHED
```
# III. Routage statique

## 1. Préparation des hôtes (vos PCs)

## 2. Configuration du routage

PC1 : ```route add 192.168.102.0/24 mask 255.255.255.0 192.168.112.2```
PC2 : ```route add 192.168.101.0/24 mask 255.255.255.0 192.168.112.1```

VM1 : ```ip route add 192.168.112.0/30 via 192.168.101.1 dev enp0s8```
VM2 : ```ip route add 192.168.112.0/30 via 192.168.102.1 dev enp0s8```

## 3. Configuration des noms de domaine

Après avoir configuré les noms de domaine sur les VM et sur les machines hôtes, on refait la root avec les noms donnés précédement. 
Puis avec la commande :
```
ping 'Nom de domaine'
```
On ping l'autre VM

![](https://github.com/GratinDauphinoi/CCNA_TP3/blob/master/ping%20vm1.PNG?raw=true)
