# Permet de connaitre le nom d la release 
lsb_release -a

>> No LSB modules are available.
>> Distributor ID:	Raspbian
>> Description:	Raspbian GNU/Linux 10 (buster)
>> Release:	10
>> Codename:	buster

# Permet de tout mettre la distribution à jour
sudo apt-get update
sudo apt-get upgrade --fix-missing
lsb_release -a

# Permet de mettre le fireware à jour
sudo apt-get -y dist-upgrade
uname -a
>> Linux raspberrypi 4.19.118-v7l+ #1311 SMP Mon Apr 27 14:26:42 BST 2020 armv7l GNU/Linux

sudo BRANCH=next rpi-update
sudo reboot
Linux raspberrypi 5.10.0-v7l+ #1380 SMP Mon Dec 14 16:53:51 GMT 2020 armv7l GNU/Linux

# Permet de faire le nettoyage des archives qui ne servent plus
sudo du -hs /var/cache/apt/archives
sudo apt-get clean
sudo du -hs /var/cache/apt/archives

# Temperature CPU
head -n 1 /sys/class/thermal/thermal_zone0/temp | xargs -I{} awk "BEGIN {printf \"%.2f\n\", {}/1000}"



# Installation derniere version python :
python3 -v
>> Python 3.7.3 (default, Jul 25 2020, 13:03:44) 
>> [GCC 8.3.0] on linux

sudo apt-get install -y build-essential tk-dev libncurses5-dev libncursesw5-dev libreadline6-dev libdb5.3-dev libgdbm-dev libsqlite3-dev libssl-dev libbz2-dev libexpat1-dev liblzma-dev zlib1g-dev libffi-dev
wget https://www.python.org/ftp/python/3.9.1/Python-3.9.1.tar.xz
tar xf Python-3.9.1.tar.xz
./configure --prefix=/usr/local/opt/python-3.9.1
./configure --enable-optimizations
make -j 4
sudo make altinstall
cd ..
sudo rm -r Python-3.9.0
rm Python-3.9.0.tar.xz
. ~/.bashrc
sudo update-alternatives --config python
python -V




# Installation de mosquitto pour les flux MQ
sudo apt-get install -y mosquitto mosquitto-clients

# Test simple
mosquitto_sub -h localhost -t test_channel
mosquitto_pub -h localhost -t test_channel -m "Hello Raspberry"

# Test securise
cd /etc/mosquitto
# -c creer le user -b ajoute un user -D delete 
sudo mosquitto_passwd -c fileAuth user
# Dans le fichier de paramétrage
sudo nano mosquitto.conf
# Modifier 
allow_anonymous false
password_file /etc/mosquitto/fileAuth
# restart
sudo reboot
sudo mosquitto_passwd -b fileAuth "Nuser" "PassUser"
mosquitto_pub -h localhost -t test -m "demo securise" -u Nuser -P PassUser
mosquitto_sub -h localhost -v test_channel -u Nuser -P PassUser
# Service
sudo service mosquitto stop
sudo service mosquitto start

# https://www.codeflow.site/fr/article/how-to-install-and-secure-the-mosquitto-mqtt-messaging-broker-on-debian-9
# Mot de passe chiffré
# Creer le fichier
/etc/mosquitto/conf.d/default.conf
# Avec ce contenu il faut bien sur les fichier cote openssl par exemple
. . .
listener 1883 localhost

listener 8883
certfile /etc/letsencrypt/live//cert.pem
cafile /etc/letsencrypt/live//chain.pem
keyfile /etc/letsencrypt/live//privkey.pem
mosquitto_pub -h  -t test -m "hello again" -p 8883 --capath /etc/ssl/certs/ -u "" -P ""
