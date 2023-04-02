configurar debian para conectarse con open ssh
1. crear un respaldo de sources.list de debian
cp /etc/apt/sources.list .
2. actualizar el repositorio de /etc/apt/sources.list
# Repositorio base estable.
deb http://deb.debian.org/debian/ buster main contrib non-free
deb-src http://deb.debian.org/debian/ buster main contrib non-free
 
# Repositorio de actualizaciones de seguridad
deb http://security.debian.org/debian-security buster/updates main contrib non-free
deb-src http://security.debian.org/debian-security buster/updates main contrib non-free
 
# Repositorio de actualizaciones anteriormente conocido como "Volátil"
deb http://deb.debian.org/debian/ buster-updates main contrib non-free
deb-src http://deb.debian.org/debian/ buster-updates main contrib non-free
 
# Backports contrib
deb http://deb.debian.org/debian buster-backports main contrib non-free
deb-src http://deb.debian.org/debian buster-backports main contrib non-free
 
# Repositorio multimedia
deb http://www.deb-multimedia.org buster main non-free

################################################################################

3. guardar cambios en el repositorio de sources.list
4. realizar la actualizacion del sistema con apt update
5. instalar el programa de openssh-server openssh-client
6. crear el respaldo de seguridad del fichero ssh
cp /etc/ssh/sshd_config .
7. configurar el adaptador de red 
nano /etc/network/interface
# The loopback network interface
auto enp0s3
iface enp0s3 inet static
address 192.168.21.5
netmask 255.255.255.0
network 192.168.21.0
broadcast 192.168.21.255
8. Guardar los cambios y reiniciar el servicio de networking
 systemctl restart networking | service networking restart
 si no reconoce service crear el PATH
 PATH=$PATH:/sbin
 despues detener el servicio con 
 systemctl stop networking
 systemctl start networking
 9. para verificar que si cambio la IP se utiliza ip add
 2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 08:00:27:31:df:08 brd ff:ff:ff:ff:ff:ff
    inet 10.0.2.15/24 brd 10.0.2.255 scope global dynamic noprefixroute enp0s3
       valid_lft 80497sec preferred_lft 80497sec
    inet 192.168.21.5/24 brd 192.168.21.255 scope global enp0s3
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fe31:df08/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever
############################################################################
wget https://dev.mysql.com/get/mysql-apt-config_0.8.22-1_all.deb
sudo apt -y install ./mysql-apt-config_0.8.22-1_all.deb
apt update
apt install mysql-server
sudo apt -y install mysql-community-server
###############################################################################
sudo ln -s /etc/nginx/sites-available/preprod.example.com /etc/nginx/sites-enabled/
sudo unlink /etc/nginx/sites-enabled/example.com
############################################################################
Alt+Shift+3 : Muestra los números de línea a la izquierda del texto en nano
