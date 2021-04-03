# Steps to deploy owncloud

**Step 1 - Install necessary updates (its always good to keep your system updated)**

```bash
sudo apt-get update

sudo apt-get upgrade
```

**Step 2 - Install all the necessary dependencies / libraries for this project** 

```bash
sudo apt-get install apache2 libapache2-mod-php7.2 openssl php-imagick php7.2-common php7.2-curl php7.2-gd php7.2-imap php7.2-intl php7.2-json php7.2-ldap php7.2-mbstring php7.2-mysql php7.2-pgsql php-smbclient php-ssh2 php7.2-sqlite3 php7.2-xml php7.2-zip
```

**Step 3 - Check Apache installation**

```bash
sudo dpkg -l apache2
```

**Step 4 - Enable apache to start on boot**

```bash
sudo systemctl start apache2

sudo systemctl enable apache2
```

**Step 5 - Check if the server is working or not**

https:/server-ip

Write this in your URL bar and check if the server is working or not

**Step 6 - Check if php is installed or not**

```bash
php -v
```

**Step 7 - Install MariaDB database**

```bash
sudo apt install mariadb-server
```

The maria db installation is not secure as it is a public database, so for a secure connection use:

```bash
sudo mysql_secure_installation
```

Now we need to answer various questions regarding removal of access of anonymous users: Say YES to all of them (if you feel you don't need it you may answer NO to the choices)

**Step 8 - Create a owncloud database**

```bash
sudo mysql --user=root mysql
```

Create root user

```bash
CREATE USER 'owncloud_db'@'localhost' IDENTIFIED BY 'naren99';
```

Grant all privileges to root user

```bash
GRANT ALL PRIVILEGES ON *.* TO 'owncloud_db'@'localhost' WITH GRANT OPTION;
```

//when we grant some privileges for a user, running the command flush privileges will reload the grant tables in the mysql database enabling the changes to take effect without reloading or restarting

```bash
FLUSH PRIVILEGES;
EXIT;
```

---

MySQL details:

Username: owncloud_db

Password: {enter a password}

Database: owncloud_db

Server: localhost

**Step 9 - Download OwnCloud**

```bash
sudo wget [https://download.owncloud.org/community/owncloud-10.4.0.zip](https://download.owncloud.org/community/owncloud-10.4.0.zip)

sudo unzip owncloud-10.4.0.zip -d /var/www/

sudo chown -R www-data:www-data /var/www/owncloud/

sudo chmod -R 755 /var/www/owncloud/
```

**Step 10 - Configure Apache for OwnCloud**

```bash
sudo nano /etc/apache2/conf-available/owncloud.conf
```

**Add the configuration below:**

```bash
Alias /owncloud “/var/www/owncloud/”

<Directory /var/www/owncloud/>

Options +FollowSymlinks

AllowOverride All

<ifModule mod_dav.c>

Dav off

</ifModule>

SetEnv HOME /var/www/owncloud

SetEnv HTTP_HOME /var/www/owncloud

</Directory>
```

Save and close the file.

Next, you need to enable all the required Apache modules and the newly added configuration by running the commands below:

```bash
sudo a2enconf owncloud

sudo systemctl reload apache2

sudo a2enmod rewrite

sudo systemctl restart apache2

sudo a2enmod headers

sudo a2enmod env

sudo a2enmod dir

sudo a2enmod mime

sudo systemctl restart apache2
```

**Step 11 - Mounting and Setting up an external hard drive**

Having an NTFS drive we will need to install a NTFS package by entering the following:

```bash
sudo apt-get install ntfs-3g
```

Make a directory we can mount to:

```bash
sudo mkdir /media/ownclouddrive
```

Create and add the www-data user to the www-data group:

```bash
sudo groupadd www-data

sudo usermod -a -G www-data www-data
```

Make the user www-data owner of the mounted drive and make its permissions read, write and execute:

```bash
sudo chown -R www-data:www-data /media/ownclouddrive

sudo chmod -R 775 /media/ownclouddrive

sudo chmod -R 777 /media/ownclouddrive
```

Now we need to get the gid, uid, and the uuid as we will need to use them so the pi will remember it even if we plug it into a different USB port. Enter the following command for the gid:

```bash
id -g www-data
```

Now to get the uid enter the following command:

```bash
id -u www-data
```

Also we need to get the UUID of the attached external hard drive so the Pi can remember this drive even if you plug it into a different USB port.

```bash
ls -l /dev/disk/by-uuid
```

The copy the light blue letters and numbers of the sda1 entry usually located on the bottom. Should look something like (numbers&letters -> ../../sda1).**(FCFCEE4DFCEE022E)**

```bash
sudo fdisk -l

df -h

ls -l /dev/disk/by-uuid
```

Now add your drive into the fstab file so it’ll boot with the proper permissions:

```bash
sudo nano /etc/fstab
```

Add the following line to the bottom of the file, updating uid, guid and the UUID with the values we got above. (It should all be a single line); Don’t forget to replace the UUID number to yours instead of the one you copied from here:

UUID=FCFCEE4DFCEE022E /media/ownclouddrive auto nofail,uid=33,gid=33,umask=0027,dmask=0027,noatime 0 0

Reboot the Raspberry Pi:

```bash
sudo reboot
```

Now the drives should automatically be mounted. If mounted we’re all good to fo. To check it enter:

```bash
sudo ls /media/ownclouddrive

df -h
```

**Step 12 - Finalizing the OwnCloud Installation**

Type in your server’s address followed by the /owncloud suffix.

[http://server-IP/owncloud](http://server-ip/owncloud)

---

Create admin account

Username: admin

Password: {enter your password}

---

Datafolder: /media/ownclouddrive

Configure MySQL/MariaDB database with the details

Press finish setup and wait until setup is complete

---

Wait for first login

---

Add some new file for testing out the storage features
