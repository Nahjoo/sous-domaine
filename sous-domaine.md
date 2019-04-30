
# Configuration du domaine et des DNS
        Mon nom de domaine est chez OVH, je vais donc sur l�interface de mon nom de domaine, dans la zone DNS, puis j�ajoute une entr�e de type CNAME.

        Mettre le nom de ton sous-domaine et pointer vers WWW comme sur l'image

image

## Ensuite sur ton vps , tu va dans 
	
	* cd /etc/apache2/sites-available/

## tu crée un fichier :

	* sudo nano nom_sous_domaine.domaine(.com).conf

## dans ce fichier tu colle, oublie pas de remplacer "nom_sous_domaine.domaine(.com)" par ton sous-domaine / exemple : sous-domaine.mathias.com :

	

        <VirtualHost *:80>

                ServerAdmin contact@nom_sous_domaine.domaine(.com)
                ServerName nom_sous_domaine.domaine(.com)

                DocumentRoot /var/www/html/(ici tu mets le dossier public)/
                <Directory /var/www/html/(ici tu mets le dossier public)/>
                        Options Indexes FollowSymLinks MultiViews
                </Directory>

                ErrorLog /var/log/apache2/nom_sous_domaine.domaine(.com)-error.log

                # Possible values include: debug, info, notice, warn, error, crit,

                # alert, emerg.

                LogLevel warn
                CustomLog /var/log/apache2/nom_sous_domaine.domaine(.com)-access.log combined
                ServerSignature On

        RewriteEngine on
        RewriteCond %{SERVER_NAME} =nom_sous_domaine.domaine(.com)
        RewriteRule ^ https://%{SERVER_NAME}%{REQUEST_URI} [END,NE,R=permanent]
        </VirtualHost>

## Ensuite tape ces 2 commandes :

        sudo a2ensite nom_sous_domaine.domaine(.com)
        sudo service apache2 restart