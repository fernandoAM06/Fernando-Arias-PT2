# Practica 2
## Configuració del sistema de virtualització (IsardVDI)
En primer pas accedim a la plataforma IsardVDI amb el nostre usuari.

Fem clic a Crear nova màquina virtual i configurem:
Sistema operatiu: Ubuntu Server .
Guardem i iniciem la màquina virtual.

# Instal·lació de LAMP stack a Ubuntu 24.04
Per instal·lar una pila LAMP (Linux, Apache, MySQL, PHP) a Ubuntu 24.04, segueix aquests passos detallats. Aquesta guia assumeix que comences amb un sistema net d’Ubuntu 24.04 i tens privilegis `sudo`.

### 1. **Actualitza el sistema**
```bash
sudo apt update && sudo apt upgrade -y
```

### 2. **Instal·la Apache**

```bash
sudo apt install apache2 -y
```

**Activa i inicia el servei:**
```bash
sudo systemctl enable apache2
sudo systemctl start apache2
```

**Verifica l’estat:**
```bash
sudo systemctl status apache2
```

Visita `http://localhost` per veure la pàgina per defecte d’Apache.

### 3. **Instal·la MySQL**

Ubuntu 24.04 ja inclou el paquet `mysql-server` als repositoris oficials (versió 8.0 o superior):

```bash
sudo apt install mysql-server mysql-client -y
```

**Inicia i habilita el servei:**
```bash
sudo systemctl enable mysql
sudo systemctl start mysql
```
**Configura de MySQL:**

#### Accés a la consola de MySQL
```bash
sudo mysql
```

#### Creació de la base de dades
```sql
CREATE DATABASE bbdd;
```

#### Creació de l’usuari local
```sql
CREATE USER 'usuario'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
GRANT ALL PRIVILEGES ON bbdd.* TO 'usuario'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```

> **Nota:** Aquest usuari només pot connectar-se des del servidor local (`localhost`), cosa que és suficient si l’aplicació web i la base de dades estan al mateix servidor.

### 4. **Instal·la PHP i extensions comunes**

Ubuntu 24.04 inclou PHP 8.3 als repositoris estàndard:

```bash
sudo apt install php libapache2-mod-php php-mysql php-curl php-gd php-mbstring php-xml php-zip php-json php-cli -y
```

**Reinicia Apache per carregar PHP:**
```bash
sudo systemctl restart apache2
```

**Verifica la versió de PHP:**
```bash
php -v
```

**Crea un fitxer de prova:**
```bash
echo "<?php phpinfo(); ?>" | sudo tee /var/www/html/info.php
```

Visita `http://localhost/info.php` per veure la informació de PHP.

> 🔒 **Mesura de seguretat:** Un cop hagis verificat que funciona, elimina el fitxer:
> ```bash
> sudo rm /var/www/html/info.php
> ```

### Verificació final

# Guia d’instal·lació i configuració de plataformes cloud (Nextcloud / ownCloud)  
**Dins d’un virtual host preconfigurat (`/var/www/domini.local`)**

Aquesta guia explica com instal·lar **Nextcloud** o **ownCloud** en un entorn on ja tens un **virtual host actiu** apuntant a `/var/www/domini.local` (per exemple, `domini.local`). No cal configurar Apache ni el virtual host, ja que es considera ja operatiu.

## 1. Descàrrega i instal·lació de la plataforma cloud

### 1.1. Enllaços oficials

- **Nextcloud**: [https://www.nextcloud.com](https://www.nextcloud.com)  
  Descàrrega directa:  
  [https://download.nextcloud.com/server/releases/latest.zip](https://download.nextcloud.com/server/releases/latest.zip)

- **ownCloud**: [https://www.owncloud.org](https://www.owncloud.org)  
  Descàrrega directa (versió estable):  
  [https://download.owncloud.com/server/stable/owncloud-complete-20240724.zip](https://download.owncloud.com/server/stable/owncloud-complete-20240724.zip)

> **Nota**: Nextcloud és compatible amb PHP 8.1+, mentre que **ownCloud encara requereix PHP 7.4** en moltes versions estables. Assegura’t de tenir la versió de PHP adequada abans d’instal·lar.


### 1.2. Passos d’instal·lació

1. **Mou’t al directori del virtual host**:
   ```bash
   cd /var/www/domini.local
   ```
2. **Neteja el contingut actual** (si cal):
   > Assegura’t que no hi ha dades importants abans d’executar això.
   ```bash
   sudo rm -rf *
   ```
   
3. **Descarrega el fitxer `.zip`** de la plataforma triada (Nextcloud o ownCloud) al teu sistema.
    ```bash
    wget https://download.nextcloud.com/server/releases/latest.zip
   ```

4. **Descomprimeix l’arxiu directament al directori**:

   - **Heu descarregat l'arxiu a una ruta qualsevol**
   ```bash
   sudo unzip /ruta/al/arxiu.zip
   ```
   > Si l’arxiu crea una carpeta interna (ex: `nextcloud/` o `owncloud/`), assegura’t que el contingut es mogui **al nivell arrel** del virtual host:
   ```bash
   sudo mv nextcloud/* . && sudo rmdir nextcloud
   # o
   sudo mv owncloud/* . && sudo rmdir owncloud
   ```

   - **Podeu fer això directament si ho teniu descomprimit a `Descargas`:**
   ```bash
   cp -R ~/Descargas/nextcloud/. /var/www/domini.local/.
   ```
   Elimineu la carpeta `nextcloud` i l'arxiu `latest.zip`
    ```bash
    sudo rm -rf ~/Descargas/nextcloud && sudo rm -rf ~/Descargas/latest.zip
    ```

   - **Podeu fer això directament si ho teniu descomprimit a `/var/www/domini.local`:**
   ```bash
   cp -R /var/www/domini.local/nextcloud/. /var/www/domini.local/.
   ```
   Elimineu la carpeta `nextcloud` i l'arxiu `latest.zip`
    ```bash
    sudo rm -rf /var/www/domini.local/nextcloud && sudo rm -rf /var/www/domini.local/latest.zip
    ```
6. **Assegura els permisos correctes**:
   ```bash
   sudo chown -R www-data:www-data /var/www/domini.local
   sudo chmod -R 755 /var/www/domini.local
   ```

7. **Accedeix a la interfície web**:
   Obre el navegador i visita:
   ```
   http://domini.local
   ```
   Segueix les instruccions de configuració assistida:
   - Crea un usuari administrador.
   - Configura la base de dades (recomanat: MariaDB/MySQL).
   - Verifica que tots els requisits del sistema es compleixin.

## 2. Recomanacions addicionals

- **Directori de dades**: Durant la instal·lació, es recomana **no emmagatzemar les dades dins del directori web** (ex: `/var/www/domini.local/data`). Millor usa una ruta externa com `/var/ncdata` o `/opt/owncloud-data`.
- **Còpies de seguretat**: Fes *backups* regulars del directori de dades i de la base de dades.
- **Seguretat**: Desactiva l’accés a fitxers sensibles (`.htaccess`, `config.php`) i considera afegir regles de seguretat addicionals a Apache o Nginx.


## Apèndix: Instal·lació de PHP 7.4 a Ubuntu 24.04 (només per a ownCloud)

> **Aquest pas només és necessari si instal·les ownCloud**, ja que moltes versions estables encara no són compatibles amb PHP 8.3 (versió per defecte a Ubuntu 24.04). Nextcloud **no requereix aquest pas**.

### Passos:

1. **Actualitza el sistema**:
   ```bash
   sudo apt update && sudo apt upgrade -y
   ```

2. **Instal·la les dependències per afegir repositoris PPA**:
   ```bash
   sudo apt install software-properties-common -y
   ```

3. **Afegeix el repositori de PHP de Ondřej Surý**:
   ```bash
   LC_ALL=C.UTF-8 sudo add-apt-repository ppa:ondrej/php -y
   ```

4. **Actualitza els repositoris**:
   ```bash
   sudo apt update
   ```

5. **Instal·la PHP 7.4 i les extensions requerides**:
   ```bash
   sudo apt install -y php7.4 \
       libapache2-mod-php7.4 \
       php7.4-fpm \
       php7.4-common \
       php7.4-mbstring \
       php7.4-xmlrpc \
       php7.4-soap \
       php7.4-gd \
       php7.4-xml \
       php7.4-intl \
       php7.4-mysql \
       php7.4-cli \
       php7.4-ldap \
       php7.4-zip \
       php7.4-curl
   ```

6. **(Opcional) Selecciona PHP 7.4 com a versió per defecte**:
   ```bash
   sudo update-alternatives --config php
   ```

7. **Activa els mòduls d’Apache necessaris**:
   ```bash
   sudo a2enmod proxy_fcgi setenvif
   sudo a2enconf php7.4-fpm
   ```

8. **Reinicia Apache**:
   ```bash
   sudo systemctl restart apache2
   ```

> **Verificació**: Pots comprovar la versió activa de PHP amb:
> ```bash
> php -v
> ```

