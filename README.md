# Airssl 2.1 - Nyzo adaptation
...
# Installation
## Configuration
Work on Ubuntu 14.04 and less
## Required packages
Driftnet, Ettercap, DHCP, Aircrack and SSLStrip
```sh
$ su root
$ apt-get update
$ apt-get upgrade
$ apt-get install driftnet ettercap-graphical isc-dhcp-server sslstrip aircrack-ng
```
## Install
Clone git repositery :
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
# Bug fixes
...
