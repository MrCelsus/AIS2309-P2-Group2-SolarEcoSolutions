# INSTALLATION D’UN SERVEUR GLPI

  

#### ::✔️ INSTALLATION DU SERVEUR::

  

📌 **PRÉ - REQUIS**

  

Debian server

  

**📌CONFIGURATION**

  

Faire une mise-à-jour :

  

```other

sudo apt-get update && sudo apt-get upgrade

```

  

Installation d'Apache :

  

```other

sudo apt-get install apache2 -y

```

  

Activation d'Apache au démarrage de la machine :

  

```other

sudo systemctl enable apache2

```

  

Installation de la base de donnée. Ici nous installons **MariaDB** :

  

```other

sudo apt-get install mariadb-server -y

```

  

Installation des modules annexes :

  

```other

sudo apt-get install php libapache2-mod-php -y

sudo apt-get install php-{ldap,imap,apcu,xmlrpc,curl,common,gd,json,mbstring,mysql,xml,intl,zip,bz2}

```

  

**📌 CONFIGURATON MARIA DB**

  

**L**a commande ci-dessous va lancer le processus d'initialisation de la base de données :

  

```other

sudo mysql_secure_installation

```

  

Répondre `Y` à toutes les questions qui seront posées pendant l'initialisation.

  

Suite à la question `Change the root password?` il faudra entrer le mot de passe de la base de données.

  

> ⚠️ Attention : retenir ce mot de passe car il te sera demandé plus tard dans l'installation

  

Connexion à la base de données :

  

```other

mysql -u root -p

```

  

Suite à cette commande, retenir le mot de passe root.

  

On va configurer ceci :

  

- Un nom de base de données : `glpidb`

- un compte avec des droits d'accès élevé : `glpi` (il faudra choisir un mot de passe)

  

Cela va se faire avec les commandes ci-dessous :

  

```other

create database glpidb character set utf8 collate utf8_bin;

grant all privileges on glpidb.* to glpi@localhost identified by 'motDePasse';

flush privileges;

quit

```

  

**📌 RÉCUPÉRATION DES RESSOURCES GLPI**

  

On récupère la source :

  

```other

wget https://github.com/glpi-project/glpi/releases/download/10.0.2/glpi-10.0.2.tgz

```

  

Mettre le contenu téléchargé dans un autre emplacement :

  

Nom de domaine glpi

  

Lier le serveur GLPI au domaine BillU.lan

  

```other

sudo mkdir /var/www/glpi.BillU.lan

sudo tar -xzvf glpi-10.0.2.tgz

sudo cp -R glpi/* /var/www/glpi.BillU.lan/

```

  

Modifier les droits :

  

```other

sudo chown -R www-data:www-data /var/www/glpi.monNomDeDomaine/

sudo chmod -R 775 /var/www/glpi.monNomDeDomaine/

```

  

**📌 CONFIGURATION DE PHP**

  

On va tout d'abord éditer le fichier `php.ini` qui est sous `/etc/php/8.1/apache2/`

  

Ensuite on va modifier les paramètres suivants :

  

- memory_limit = `64M`

- file_uploads = `on`

- max_execution_time = `600`

- session.auto_start = `0`

- session.use_trans_sid = `0`

  

**📌 DONNER A L'UTILISATEUR LE CONTROLE TOTAL SUR LE RÉPERTOIRE GLPI ET SES FICHIERS**

  

```shell

sudo mv glpi /var/www/html/

```

  

Créez un fichier de configuration Apache nommé glpi.conf

  

```shell

sudo nano /etc/apache2/conf-available/glpi.conf

```

  

Voici le fichier avec notre configuration.

  

[glpi.conf.rtf](https://res.craft.do/user/full/7f128f79-9318-996c-52fb-ce9d606b485a/EE5B08E6-0396-4C61-9C62-A00FB7BC7571_2/mvHZX4kdvyjL6xrOgCbD47tALlHUzn01ENz4PL8oAMkz/glpi.conf.rtf)

  

Activer la nouvelle configuration sur Apache.

  

```shell

sudo a2enconf glpi

```

  

Redémarrez le serveur Web Apache manuellement.

  

```shell

sudo service apache2 restart

```

  

Ouvrez votre navigateur et entrez l'adresse IP de votre serveur Web plus / glpi.

  

**📌 MODIFIER LE SITE PAR DÉFAUT D’APACHE**

  

Modifier le fichier situé suivant : `/etc/apache2/sites-available/000-default.conf`

  

```shell

sudo nano /etc/apache2/sites-available/000-default.conf

```

  

Modifier la ligne `DocumentRoot /var/www/html` par `DocumentRoot /var/www/html/glpi`

  

> ⚠️ Si vous tombez sur une page web d’Apache par défaut, vous pouvez supprimer le fichier index.html avec la commande suivante et rafraichir la page, vous sera alors bien sur le setup d’installation de GLPI : rm /var/www/html/index.html

  

#### ::✔️ LIAISON AVEC ACTIVE DIRECTORY::

  

Connectez-vous en tant que s**uper-admin** *(compte glpi par défaut)* sur l’**interface web de GLPI**. Rendez-vous dans le **menu Administration** puis dans **Authentification**.

  

![glpi-ldap4.png](https://neptunet.fr/wp-content/uploads/2020/11/glpi-ldap4.png)

  

Cliquez sur **Annuaires LDAP**.

  

![glpi-ldap5.png](https://neptunet.fr/wp-content/uploads/2020/11/glpi-ldap5.png)

  

Il faut **ajouter un annuaire** pour créer la liaison. Pour cela, cliquez sur le symbole **+** situé dans la barre du haut.

  

![glpi-ldap6.png](https://neptunet.fr/wp-content/uploads/2020/11/glpi-ldap6.png)

  

Il faut maintenant **remplir différentes informations** qui vont permettre à GLPI de communiquer avec le contrôleur de domaine. GLPI propose de **remplir certains champs automatiquement**, dont le champ **Filtre de connexion**! Pour cela, cliquez sur « **Active Directory** » dans la ligne **Préconfiguration.**

  

![glpi-ldap7.png](https://neptunet.fr/wp-content/uploads/2020/11/glpi-ldap7.png)

  

Les zones **Filtre de connexion, champ de l’identifiant et champ de synchronisation ont été remplies**. Ces 3 zones permettent de définir comment seront recherchés les utilisateurs dans la base de données AD et quels seront les attributs d’un objet utilisateur utilisés pour se connecter.

  

![glpi-ldap8.png](https://neptunet.fr/wp-content/uploads/2020/11/glpi-ldap8.png)

  

Complétez le formulaire avec les informations de votre domaine comme ceci :

  

- **Nom** : *BillU.lan*

- **Serveur par défaut** : mettre **Oui**

- **Actif** : mettre **Oui** pour activer la liaison entre le serveur et GLPI

- **Serveur** : renseignez l’adresse **IP du serveur 172.168.2.4 ou son nom complet** avec le nom du domaine srv-main.BillU.lan

- **Port** : par défaut, le protocole LDAP utilise le **port 389**. Si vous n’avez pas modifié ce port dans votre infrastructure, **laissez par défaut.**

- **BaseDN** : renseignez le **Distinguished Name de l’Unité d’Organisation dont vous voulez importer les utilisateurs** ou le **Distinguished Name du domaine entier** si vous souhaitez tout importer *(au format « OU=monOU,DC=domaine,DC=com » ou simplement « DC=domaine,DC=com » pour le domaine entier)*

- **DN du compte** : renseignez ici l’**identifiant complet utilisateur ayant les droits d’accès sur le domaine**

- **Mot de passe du compte** : ajoutez le mot de passe de l’utilisateur déclaré dans le champ précédent

  

Cela devrait donner cette configuration :

  

![glpi-ldap9.png](https://neptunet.fr/wp-content/uploads/2020/11/glpi-ldap9.png)

  

Quand vous avez terminé de remplir les différents champs, cliquez sur le **bouton Ajouter**. L’annuaire LDAP que vous venez de configurer sera ajouté à la liste. Une **infobulle** en bas à droite de la page web va s’afficher indiquant qu’un **test a été effectué et qu’il a réussi** si toutes les informations sont bonnes.

  

![glpi-ldap10.png](https://neptunet.fr/wp-content/uploads/2020/11/glpi-ldap10.png)

  

> ✅ A partir de ce point, **la configuration du serveur est terminée**. Les utilisateurs du domaine pourront s’identifier directement. Leurs informations seront **ajoutées automatiquement à GLPI**.

  

> ✅ Après avoir saisi l’identifiant de mon utilisateur et son mot de passe, il aura bien accès à GLPI avec par défaut un **profil « Self-Service »** dans lequel il ne pourra que **créer et suivre l’état de ses propres tickets et accéder à la FAQ.**

  

::**✔️ IMPORTER TOUS LES UTILISATEURS DE LA BASE DN**::

  

Pour importer tous les utilisateurs de la Base DN déclaré lors de la configuration afin qu’ils soient synchronisés avec GLPI avant leur première connexion.

  

Toujours dans le sous-menu Utilisateurs, cliquez sur le **bouton Liaison annuaire LDAP**.

  

![glpi-ldap16.png](https://neptunet.fr/wp-content/uploads/2020/11/glpi-ldap16.png)

  

Cliquez sur I**mportation de nouveaux utilisateurs**.

  

![glpi-ldap17.png](https://neptunet.fr/wp-content/uploads/2020/11/glpi-ldap17.png)

  

Sauf si vous souhaitez importer un utilisateur bien précis, cliquez simplement sur le **bouton Rechercher sans définir de critère.**

  

![glpi-ldap18.png](https://neptunet.fr/wp-content/uploads/2020/11/glpi-ldap18.png)

  

Vous verrez apparaître en bas de la page, tous les utilisateurs qui sont dans la **BaseDN déclarée** *(soit ceux d’une OU, soit tous les utilisateurs du domaine selon votre configuration).*

  

![glpi-ldap19.png](https://neptunet.fr/wp-content/uploads/2020/11/glpi-ldap19.png)

  

Pour les importer dans GLPI, **cochez les cases sur la gauche pour les sélectionner**, cliquez sur le **bouton Actions**, sélectionnez **Importer** puis cliquez sur **Envoyer**. Une fois encore, une infobulle vous informera du déroulement de l’import.

  

![glpi-ldap20.png](https://neptunet.fr/wp-content/uploads/2020/11/glpi-ldap20.png)

  

Si vous allez vérifier vos utilisateurs, **ils apparaitront bien dans GLPI**.

  

![glpi-ldap21.png](https://neptunet.fr/wp-content/uploads/2020/11/glpi-ldap21.png)

  

Vous pouvez également **importer des groupes AD**, les manipulations restent les mêmes.

  

![glpi-ldap22.png](https://neptunet.fr/wp-content/uploads/2020/11/glpi-ldap22.png)

  

Les groupes importés depuis l’AD seront **disponibles dans GLPI**.

  

![glpi-ldap23.png](https://neptunet.fr/wp-content/uploads/2020/11/glpi-ldap23.png)

  

---