## 1. Descàrrega i instal·lació de la plataforma cloud
1.1. Enllaços oficials
Nextcloud: https://www.nextcloud.com
Descàrrega directa:
https://download.nextcloud.com/server/releases/latest.zip

ownCloud: https://www.owncloud.org
Descàrrega directa (versió estable):
https://download.owncloud.com/server/stable/owncloud-complete-20240724.zip

Nota: Nextcloud és compatible amb PHP 8.1+, mentre que ownCloud encara requereix PHP 7.4 en moltes versions estables. Assegura’t de tenir la versió de PHP adequada abans d’instal·lar.

1.2. Passos d’instal·lació
Mou’t al directori del virtual host:

cd /var/www/domini.local
Neteja el contingut actual (si cal):

Assegura’t que no hi ha dades importants abans d’executar això.

sudo rm -rf *
Descarrega el fitxer .zip de la plataforma triada (Nextcloud o ownCloud) al teu sistema.

wget https://download.nextcloud.com/server/releases/latest.zip
Descomprimeix l’arxiu directament al directori:

Heu descarregat l'arxiu a una ruta qualsevol
sudo unzip /ruta/al/arxiu.zip
Si l’arxiu crea una carpeta interna (ex: nextcloud/ o owncloud/), assegura’t que el contingut es mogui al nivell arrel del virtual host:

sudo mv nextcloud/* . && sudo rmdir nextcloud
# o
sudo mv owncloud/* . && sudo rmdir owncloud
Podeu fer això directament si ho teniu descomprimit a Descargas:
cp -R ~/Descargas/nextcloud/. /var/www/domini.local/.
Elimineu la carpeta nextcloud i l'arxiu latest.zip

sudo rm -rf ~/Descargas/nextcloud && sudo rm -rf ~/Descargas/latest.zip
Podeu fer això directament si ho teniu descomprimit a /var/www/domini.local:
cp -R /var/www/domini.local/nextcloud/. /var/www/domini.local/.
Elimineu la carpeta nextcloud i l'arxiu latest.zip

sudo rm -rf /var/www/domini.local/nextcloud && sudo rm -rf /var/www/domini.local/latest.zip
Assegura els permisos correctes:

sudo chown -R www-data:www-data /var/www/domini.local
sudo chmod -R 755 /var/www/domini.local
Accedeix a la interfície web: Obre el navegador i visita:

http://domini.local
Segueix les instruccions de configuració assistida:

Crea un usuari administrador.
Configura la base de dades (recomanat: MariaDB/MySQL).
Verifica que tots els requisits del sistema es compleixin.

