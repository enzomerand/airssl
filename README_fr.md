# Airssl 2.1 - Adapté par Nyzo
*airssl.sh* créé de faux points d'accès wifi (hotspot), utilisant Airbase-ng, sslstrip, ettercap et Driftnet si vous le shouaitez pour récupérer les images.
## Installation
### Configuration
Fonctionne sur Ubuntu 14.04 LTS et les versions antérieures, **si vous n'êtes pas en ethernet, vous devrez avoir deux cartes wifi (soit wlan0 et wlan1, généralement)**
### Paquets requis
Driftnet, Ettercap, DHCP, Aircrack et SSLStrip
```sh
$ su root
$ apt-get update
$ apt-get upgrade
$ apt-get install driftnet ettercap-graphical isc-dhcp-server sslstrip aircrack-ng
```
### Installer
Clonez le dépôt Github :
```sh
$ cd /etc/
$ clone git https://github.com/Enzo7337/airssl.git
$ chmod 755  /etc/airssl/airssl.sh
```
Si vous n'avez pas installer git :
```sh
$ apt-get install git
```
## Utiliser le script
Identifiez-vous en tant que root :
```sh
$ su root
```
Allez dans le répertoire airssl :
```sh
$ cd /etc/airssl/
```
Lancez le script :
```sh
$ ./airssl.sh
```
Et suivez les instructions (en anglais).
## Correction de bug(s)
*Contactez-moi si vous rencontrez n'importe quel bug(s), j'emploierai tout les moyens possibles pour le(s) résoudre(s)*

Parfois, au lancement du serveur DHCP, une erreur apparaît comme :
```
Can't open /etc/dhcp/dhcp.conf: permission denied
```
ou
```
Can't open /var/lib/dhcp/dhcpd.leases: permission denied.
```
ou
```
Can't open /pentest/wireless/airssl/dhcpd.conf: Permission denied
```

Si après avoir vérifier les permissions cela affiche toujours un message d'erreur, vérifiez **apparmor** :
```sh
$ sudo apparmor_status
```

Si **/usr/sbin/dhcpd** est présent dans la liste, suivez ces instructions :
1. Arrêtez apparmor
```sh
$ sudo /etc/init.d/apparmor stop
```
2. Editez /etc/apparmor.d/usr.sbin.dhcpd avec les permissions root :
```sh
$ nano /etc/apparmor.d/usr.sbin.dhcpd
```
3. Et assurez-vous que le fichier contient ces lignes (peu importe l'ordre) :
```sh
  /etc/dhcp/ r,
  /etc/dhcp/** r,
  /etc/dhcpd{,6}.conf r,
  /etc/dhcpd{,6}_ldap.conf r,
  /pentest/wireless/airssl/dhcpd{,6}.conf r,

  /usr/sbin/dhcpd mr,

  /var/lib/dhcp/dhcpd{,6}.leases* lrw,
  /var/log/ r,
  /var/log/** rw,
  /{,var/}run/{,dhcp-server/}dhcpd{,6}.pid rw,
```
4. Démarrez apparmor
```sh
$ sudo /etc/init.d/apparmor start
```

Après cette opération, apparmor va autoriser le serveur DHCP à ouvrir les fichiers /etc/dhcp/dhcpd.conf or /var/lib/dhcp/dhcpd.leases ou /pentest/wireless/airssl/dhcpd.conf. Pour plus d'informations, regardez **man apparmor**
