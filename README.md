# linux-config

1) Ip: 18.194.117.48,
port: 2200,
URL : http://ec2-18-194-117-48.eu-central-1.compute.amazonaws.com/

2) Software installed : 
apache2,
libapache2-mod-wsgi,
postgresql,
sqlalchemy,
flask,
git,
pip,
virtual environment,

3)Key Location: home/grader/.ssh/authorized_keys

4)login: ssh grader@18.194.117.48 -p 2200 -i ~/.ssh/authorized_key

steps:
*creating grader user

$sudo adduser grader
$ sudo nano /etc/sudoers.d/grader
$ grader ALL=(ALL) NOPASSWD:ALL
$ssh-keygen (on local machine)
$ mkdir .ssh
$ touch .ssh/authorized_keys
$ nano .ssh/authorized_keys (pasting the key and save the file)
$ chmod 700 .ssh
$ chmod 644 .ssh/authorized_keys

*update the server
$ sudo apt-get update
$ sudo apt-get upgrade

*configuring ports and firewall

$ sudo ufw default deny incoming
$ sudo ufw default allow outgoing
$ sudo ufw allow 2200/tcp
$ sudo ufw allow 80/tcp
$ sudo ufw allow ntp
$ sudo ufw enable

*configure timezone
$ sudo dpkg-reconfigure tzdata

*Install Apache2:
$ sudo apt-get install apache2
$ sudo apt-get install python-setuptools libapache2-mod-wsgi
$ sudo service apache2 restart

*install git
$sudo apt-get install git
$cd /var/www
$sudo mkdir catalog
$sudo chown -R grader:grader catalog
$cd catalog
$git clone https://github.com/hadeermoustafa/catalog.git catalog
$sudo nano catalog.wsgi (then configure the data inside the file)

*Install PostgreSQL

$sudo apt-get install libpq-dev python-dev
$sudo apt-get install postgresql postgresql-contrib
$sudo su - postgres
$psql
$CREATE USER catalog WITH PASSWORD 'password';
$ALTER USER catalog CREATEDB;
$CREATE DATABASE catalog WITH OWNER catalog;
$\c catalog
$REVOKE ALL ON SCHEMA public FROM public;
$GRANT ALL ON SCHEMA public TO catalog;
$\q
$exit

*virtual inviroments

$sudo pip install virtualenv

*install flask and pip

$sudo apt-get install python-pip
$Install Flask pip install Flask
$Install other project dependencies sudo pip install httplib2 oauth2client sqlalchemy psycopg2 sqlalchemy_utils
