# Sécurité et supervision réseau

## Installer un serveur Nagios Core sur Ubuntu 22.04



### 1. Installez tous les packages requis
#### sudo apt install wget unzip curl openssl build-essential libgd-dev libssl-dev libapache2- mod-php php-gd php apache2 -y

### 2. Téléchargez les fichiers d'installation de Nagios Core.
#### wget https://assets.nagios.com/downloads/nagioscore/releases/nagios-4.5.9.tar.gz

### 3. Extraire les fichiers téléchargés : 
#### sudo tar -zxvf nagios-4.5.9.tar.gz

### 4. Accédez au répertoire d’installation nagios-4.5.9

### 5. Exécutez le script de configuration de Nagios Core : sudo ./configure

### 6. Compiler le programme principal et les CGI : sudo make all

### 7. Créer les utilisateurs et groupes système nécessaires pour que Nagios fonctionne correctement et pour gérer la sécurité: sudo make install-groups-users

### 8. ajouter l’utilisateur (www-data) dans le groupe nagios : sudo usermod -a -G nagios wwwdata

### 9. Installer Nagios: sudo make install

### 10. Initialisez tous les scripts de configuration d’installation: 
#### sudo make install-init

### 11. Configurer les droits d’accès aux commandes externes de Nagios. : 
#### sudo make installcommandmode

### 12. Installez les fichiers de configuration : 
#### sudo make install-config

### 13. Installer les fichiers d’apache2 : 
#### sudo make install-webconf

### 14. Activer la fonction rewrite dans le serveur web Apache : 
#### sudo a2enmod rewrite

### 15. Activer la configuration CGI : 
#### sudo a2enmod cgi

### 16. Redémarrer le service apache : 
#### sudo systemctl restart apache2

### 17. Créer un utilisateur administrateur du serveur Nagios et définir le mot de passe : 
#### sudo htpasswd -c /usr/local/nagios/etc/htpasswd.users « nom_utilisateur »

### 18. Installer les Plugins Nagios
#### cd ~/
#### wget https://nagios-plugins.org/download/nagios-plugins-2.4.9.tar.gz

### 19. Extraire les plugins : 
#### sudo tar -zxvf nagios-plugins-2.4.9.tar.gz

### 20. Se déplacer au répertoire des plugins

### 21. Lancer le script de configuration des plugins : 
#### sudo ./configure --with-nagiosuser= »nom_utilisateur » --with-nagios-group=« nom_groupe_utilisateur »

### 22. Compiler les plugins de Nagios Core : 
#### sudo make

### 23. Installer les plugins : 
#### sudo make install

### 24. Vérifier le fichier de configuration de Nagios : 
#### sudo /usr/local/nagios/bin/nagios -v /usr/local/nagios/etc/nagios.cfg

### 25. Démarrer le service nagios : 
#### sudo systemctl start nagios

### 26. Activez le service Nagios pour qu'il s'exécute au démarrage du système : 
#### sudo systemctl enable nagios

### 27. Se connecter à l’interface web de Nagios et tester son fonctionnement en tapant :
#### http://adresse_ip_srv_nagios/nagios

### 28. Accéder aux modules Hosts et services pour récupérer les informations pertinentes
## N.B: en cas de problème, essayer de modifier le fichier de configuration global de nagios :

#### /usr/local/nagios/etc/cgi.cfg
