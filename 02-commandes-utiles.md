-----------------------------
-----------------------------
-----------------------------
# 1 - commandes utiles
-----------------------------
-----------------------------
-----------------------------

```bash
ssh -i mysrvubuntkey.pem azureuser@172.174.194.195
sudo -i
sudo apt update
sudo apt install apache2
sudo ufw app list
sudo ufw allow 'Apache'
sudo systemctl status apache2
hostname -I
echo "http://172.174.194.195"
sudo apt-get install mysql-server
mysql -u root -p
CREATE USER 'eleve'@'localhost' IDENTIFIED BY 'eleve';
GRANT ALL PRIVILEGES ON *.* TO 'eleve'@'localhost' WITH GRANT OPTION;
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'eleve';
FLUSH PRIVILEGES;
\! clear;
DESCRIBE mysql.user;
SELECT User, Host FROM mysql.user;
SELECT user, authentication_string, plugin, host FROM mysql.user;
FLUSH PRIVILEGES;
exit
sudo apt install php libapache2-mod-php php-mysql
php -v
cd /var/www/html
touch info.php
echo "<?php phpinfo(); ?>" > info.php
echo "http://172.174.194.195/info.php"
cd -
sudo apt update
sudo apt install phpmyadmin php-mbstring php-zip php-gd php-json php-curl
echo "http://172.174.194.195/phpmyadmin/"

```


-----------------------------
-----------------------------
-----------------------------
# 2 - mydatabase.sql pour créer et remplir une table `members` :
-----------------------------
-----------------------------
-----------------------------

```sql
-- phpMyAdmin SQL Dump
-- version 4.7.4
-- https://www.phpmyadmin.net/
--
-- Host: 127.0.0.1
-- Generation Time: Mar 12, 2018 at 07:47 AM
-- Server version: 10.1.30-MariaDB
-- PHP Version: 7.1.13

SET SQL_MODE = "NO_AUTO_VALUE_ON_ZERO";
SET AUTOCOMMIT = 0;
START TRANSACTION;
SET time_zone = "+00:00";

/*!40101 SET @OLD_CHARACTER_SET_CLIENT=@@CHARACTER_SET_CLIENT */;
/*!40101 SET @OLD_CHARACTER_SET_RESULTS=@@CHARACTER_SET_RESULTS */;
/*!40101 SET @OLD_COLLATION_CONNECTION=@@COLLATION_CONNECTION */;
/*!40101 SET NAMES utf8mb4 */;

--
-- Database: `mydatabase`
--

-- --------------------------------------------------------

--
-- Table structure for table `members`
--

CREATE TABLE `members` (
  `id` int(11) NOT NULL,
  `firstname` varchar(30) NOT NULL,
  `lastname` varchar(30) NOT NULL,
  `address` text NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=latin1;

--
-- Dumping data for table `members`
--

INSERT INTO `members` (`id`, `firstname`, `lastname`, `address`) VALUES
(1, 'neovic', 'devierte', 'silay city'),
(2, 'gemalyn', 'cepe', 'carmen, bohol'),
(3, 'lee', 'apilinga', 'bacolod'),
(4, 'julyn', 'divinagracia', 'eb magalona'),
(5, 'cristine', 'demapanag', 'talisay');

--
-- Indexes for dumped tables
--

--
-- Indexes for table `members`
--
ALTER TABLE `members`
  ADD PRIMARY KEY (`id`);

--
-- AUTO_INCREMENT for dumped tables
--

--
-- AUTO_INCREMENT for table `members`
--
ALTER TABLE `members`
  MODIFY `id` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=38;
COMMIT;

/*!40101 SET CHARACTER_SET_CLIENT=@OLD_CHARACTER_SET_CLIENT */;
/*!40101 SET CHARACTER_SET_RESULTS=@OLD_CHARACTER_SET_RESULTS */;
/*!40101 SET COLLATION_CONNECTION=@OLD_COLLATION_CONNECTION */;
```


-----------------------------
-----------------------------
-----------------------------
# Commandes 3
-----------------------------
-----------------------------
-----------------------------


```bash
scp -r -i mysrvubuntukey.pem ./site azureuser@172.174.194.195:/tmp
ssh -i mysrvubuntukey.pem azureuser@172.174.194.195
sudo -i
cd /tmp
cd site
ls
cp -R * /var/www/html/
cd /var/www/html/
ls
sudo systemctl restart apache2
echo "http://172.174.194.195/"
rm /var/www/html/index.html
echo "http://172.174.194.195/index.php"
scp -i mysrvubuntukey.pem ./connection.php azureuser@172.174.194.195:/var/www/html/connection.php
sudo systemctl restart apache2
```


-----------------------------
-----------------------------
-----------------------------
# Commandes 4
-----------------------------
-----------------------------
-----------------------------

```bash
ssh -i mysrvubuntukey.pem azureuser@172.174.194.195
sudo -i
sudo apt update
sudo apt install certbot python3-certbot-apache
sudo ufw allow 'Apache Full'
sudo certbot --apache # Entrez votre nom de domaine lorsqu'il vous sera demandé
sudo systemctl status certbot.timer
sudo certbot renew --dry-run
```

### Détails des commandes :
- **`sudo apt install certbot python3-certbot-apache`** : Installe Certbot et son plugin Apache.
- **`sudo ufw allow 'Apache Full'`** : Permet le trafic HTTP et HTTPS à travers le pare-feu.
- **`sudo certbot --apache`** : Exécute Certbot avec le plugin Apache pour obtenir automatiquement un certificat SSL et configurer Apache pour l'utiliser. Il vous sera demandé de fournir un nom de domaine valide.
- **`sudo systemctl status certbot.timer`** : Vérifie le statut du timer de Certbot pour s'assurer que le renouvellement automatique est actif.
- **`sudo certbot renew --dry-run`** : Teste le processus de renouvellement pour s'assurer qu'il se passera sans problème lorsque le certificat aura besoin d'être renouvelé.
