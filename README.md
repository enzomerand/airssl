# Airssl 2.1 - Nyzo adaptation
*airssl.sh* creates a fake access point using Airbase-ng and uses sslstrip to bypass ssl encryption, it also offers the user the choice to use Driftnet to capture images. 
## Installation
### Configuration
Work on Ubuntu 14.04 and less, **if you are not ethernet, you will need two wireless cards.**
### Required packages
Driftnet, Ettercap, DHCP, Aircrack and SSLStrip
```sh
$ su root
$ apt-get update
$ apt-get upgrade
$ apt-get install driftnet ettercap-graphical isc-dhcp-server sslstrip aircrack-ng
```
### Install
Clone git repository :
```sh
$ cd /etc/
$ clone git https://github.com/Enzo7337/airssl.git
$ chmod 755  /etc/airssl/airssl.sh
```
If git is not installed
```sh
$ apt-get install git
```
## Run et use
Put yourself in as root:
```sh
$ su root
```
Go to the airssl directory :
```sh
$ cd /etc/airssl/
```
Run script :
```sh
$ ./airssl.sh
```
Follow the instructions
## Bug fixes
*Contact me if you encounter any bugs so that I correct them.*

Sometimes upon rising DHCP server informs about permission errors like
```
Can't open /etc/dhcp/dhcp.conf: permission denied
```
or
```
Can't open /var/lib/dhcp/dhcpd.leases: permission denied.
```
or
```
Can't open /pentest/wireless/airssl/dhcpd.conf: Permission denied
```

If after checking the permissions are found to be correct, check **apparmor** profile for dhcpd:
```sh
$ sudo apparmor_status
```

If **/usr/sbin/dhcpd** is in the list of profiles do the following:
1. Stop apparmor deamon
```sh
$ sudo /etc/init.d/apparmor stop
```
2. Edit /etc/apparmor.d/usr.sbin.dhcpd with root permissions :
```sh
$ nano /etc/apparmor.d/usr.sbin.dhcpd
```
3. And ensure that file has following lines:
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
4. Start apparmor deamon
```sh
$ sudo /etc/init.d/apparmor start
```

After this operation apparmor deamon will allow dhcp server to open /etc/dhcp/dhcpd.conf or /var/lib/dhcp/dhcpd.leases files. For more information see **man apparmor**


La traduction en français arrive bientôt !
