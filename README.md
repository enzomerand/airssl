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
```sh

```
or
```sh

```

```sh

```


La traduction en français arrive bientôt !
