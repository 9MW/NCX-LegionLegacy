# NCX-LegionLegacy
 VCR Legion Core 2.0 (based on uwow) => Linux Compilable

# REQUREMENTS

boost_1_60_0, openssl-1.0.0, libssl1.0-dev

```shell
#INSTALL dependencies:
# --------------------------------------------------------------------------------
apt update
apt install git clang cmake make gcc g++ libmariadbclient-dev libbz2-dev libreadline-dev libncurses-dev mariadb-server p7zip libmariadb-client-lgpl-dev-compat

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

# --------------------------------------------------------------------------------
make -j 4
make install

# --------------------------------------------------------------------------------

to be continue.........



```
