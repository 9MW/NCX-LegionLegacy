# NCX-LegionLegacy
 VCR Legion Core 2.0 (based on uwow) => Linux Compilable

# REQUREMENTS

boost_1_60_0, openssl-1.0.0, libssl1.0-dev
```shell
wget https://www.openssl.org/source/openssl-1.0.0.tar.gz
tar -xzvf openssl-1.0.0.tar.gz
cd openssl-1.0.0
sudo ./config --prefix=/usr
sudo make
sudo make test
sudo make install_sw

openssl version -v 
```

# COMPILE SERVER

```shell
#INSTALL dependencies:
# --------------------------------------------------------------------------------
apt update
apt install git clang cmake make gcc g++ libmariadbclient-dev libbz2-dev libreadline-dev libncurses-dev mariadb-server p7zip libmariadb-client-lgpl-dev-compat

apt install libboost1.67-all-dev

apt install libasio-dev
apt install libzmq3-dev 
apt install libelf-dev libdwarf-dev
apt install libbfd-dev
apt install libdw1 libdw-dev

# --------------------------------------------------------------------------------
# VEEEEEEERY IMPORTANT LIBSSL FIX:

apt-get remove libssl-dev
nano /etc/apt/sources.list

#add at end of file
deb http://security.ubuntu.com/ubuntu bionic-security main

apt update

apt install libssl1.0-dev

# --------------------------------------------------------------------------------

git clone https://github.com/nathalis/NCX-LegionLegacy
cd NCX-LegionLegacy
mkdir build
cd build

# --------------------------------------------------------------------------------
cmake ../ -DCMAKE_INSTALL_PREFIX=/root/serverlegion
# OR (extra config):
cmake ../ -DCMAKE_INSTALL_PREFIX=/root/serverlegion -DCMAKE_C_FLAGS="-m64 -D_LARGEFILE_SOURCE -D_FILE_OFFSET_BITS=64 -g3 -ggdb3 -msse3 -fno-delete-null-pointer-checks -fno-strict-aliasing -frename-registers -rdynamic" -DCMAKE_CXX_FLAGS="-m64 -D_LARGEFILE_SOURCE -D_FILE_OFFSET_BITS=64 -g3 -ggdb3 -msse3 -fno-delete-null-pointer-checks -fno-strict-aliasing -frename-registers -rdynamic" -DCMAKE_BUILD_TYPE=Release -DWITH_COREDEBUG=0 -DTOOLS=1 -DWITH_WARNINGS=0
# --------------------------------------------------------------------------------
make -j 4
make install

# --------------------------------------------------------------------------------

```

# DATABASES

```shell
# --------------------------------------------------------------------------------
#SQL INSTALL & SETUP

sudo apt update
sudo apt install mariadb-server mariadb-client

nano /etc/mysql/mariadb.conf.d/50-server.cnf
# change these lines to:

bind-address            = 0.0.0.0
innodb_strict_mode      = 0

#.............................................
sudo mysql -u root -p mysql

update user set plugin=' ' where user='root';
SET PASSWORD FOR root@localhost = PASSWORD('your_root_password');
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'your_root_password' WITH GRANT OPTION;
flush privileges;
exit

#.............................................
# NOW IMPORT DATABASES

mysql -u root -p database < file.sql

#.............................................
# NOW INSTALL PHPMYADMNIN:

apt-get install php-mbstring php-gettext

sudo add-apt-repository ppa:phpmyadmin/ppa
sudo apt-get update
sudo apt-get install phpmyadmin


# Web server to reconfigure automatically: <-- apache2
# Configure database for phpmyadmin with dbconfig-common? <-- No

# --------------------------------------------------------------------------------
# --------------------------------------------------------------------------------
```
