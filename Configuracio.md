## Funcionament del nexcloud
## 4. Demostració de funcionament:

# Pujar archius 
Ja dins de nextclud ens fiquem a la part d'arxius, i on posa un +New podem seleccionar l'arxiu que volem i guardar-ho 

![](https://github.com/fernandoAM06/Fernando-Arias-PT2/blob/main/1.foto%20aplicaciones%20web.png)

# Crear Carpetes
Per crear la carpeta tenim que anar al mateiix lloc d'aband i donar-li a new flder

![](https://github.com/fernandoAM06/Fernando-Arias-PT2/blob/main/3.Aplicacioens%20web.png)

# Compartir Continguts
Primer li donem a la carpeta que volem compartir i cliquem en la persona que tenim

![](https://github.com/fernandoAM06/Fernando-Arias-PT2/blob/main/Captura%20de%20pantalla%202025-12-04%20121651.png)
 ## 5.Creació d'usuaris
  # Crear tres usuaris
  # Documentar el procés
  En primer pas tenim que crear tres usuaris, el primer  es el rol administrador, en segon l'editor i per ultim visualizador
  Per crear el primer li donem al apartat del nostre perfil i desprès a Accounts, ja dins cliquem en New account i posem admin en els apartats que ens deixa
  ![](https://github.com/fernandoAM06/Fernando-Arias-PT2/blob/main/Captura%20de%20pantalla%202025-12-04%20122212.png)
  ![](https://github.com/fernandoAM06/Fernando-Arias-PT2/blob/main/Captura%20de%20pantalla%202025-12-04%20122558.png)
  ![](https://github.com/fernandoAM06/Fernando-Arias-PT2/blob/main/Captura%20de%20pantalla%202025-12-04%20122924.png)

Desprès creem el d'editor que es el mateix però tenim que fer un nou grup i seguidament donar-li a crear conte com abans.

![](https://github.com/fernandoAM06/Fernando-Arias-PT2/blob/main/Captura%20de%20pantalla%202025-12-09%20103340.png)
![](https://github.com/fernandoAM06/Fernando-Arias-PT2/blob/main/Captura%20de%20pantalla%202025-12-09%20103805.png!)
 Per fer el seguent tenim que seguir el mateixos pasos que l'anterior,solament cambien el nombre a visualizador
 Aqui tenim totes les contes creades:
 ![](https://github.com/fernandoAM06/Fernando-Arias-PT2/blob/main/Captura%20de%20pantalla%202025-12-09%20104458.png)

## 6.Assignació de rols i permisos
# Configurar permisos per rol
En primer pas escollim una carpeta i li donem a la persona amb un més per compartir els tres usuaris editor,admin i visualizador
En la foto podem veure como cadascu te su rol i solament tenen uns permisos determinats
 ![](https://github.com/fernandoAM06/Fernando-Arias-PT2/blob/main/Captura%20de%20pantalla%202025-12-09%20110414.png)

 ## 7.Administració d’arxius
 # Organització de carpetes i fitxers:
 En primer pas creem tres carpetes
  ![](https://github.com/fernandoAM06/Fernando-Arias-PT2/blob/main/Captura%20de%20pantalla%202025-12-09%20131825.png)
 
   En segon pas creem l'enllaç
   ![](https://github.com/fernandoAM06/Fernando-Arias-PT2/blob/main/Captura%20de%20pantalla%202025-12-09%20132110.png)

  I per ultim creem la contrasenya i data de venciment
   ![](https://github.com/fernandoAM06/Fernando-Arias-PT2/blob/main/Captura%20de%20pantalla%202025-12-09%20130823.png)

 ## 8.Accés des d’una màquina qualsevol de la xarxa
  # Configuració d'accés remot:
###  1. Configuració de la xarxa de la màquina virtual

En primer pas a  la configuració de la màquina virtual  s’ha de posar la targeta de xarxa en mode Pont (Bridge).
Aquest mode fa que la màquina virtual tingui una IP pròpia dins la mateixa xarxa que la resta d’ordinadors.

### 2. Obtenir la IP de la màquina virtual

Dins la màquina virtual:

Anar a Configuració de xarxa del sistema.

Mirar l’adreça IPv4 (per exemple: 192.168.1.50).

Aquesta IP serà la que s’utilitzarà per connectar-se.

### 3. Permetre connexions externes a Nextcloud

Perquè Nextcloud accepti connexions des d’altres dispositius:

Entrar a Nextcloud des de la pròpia màquina virtual.

Anar a Configuració de l’administrador.

Buscar l’opció Dominis de confiança (Trusted domains).

Afegir la IP de la VM (per exemple 192.168.1.50).

Així Nextcloud permetrà l’accés des de fora de la màquina virtual.

### 4. Accedir des d’un altre ordinador

Des d’un altre dispositiu connectat a la mateixa xarxa:

Obrir un navegador web.

Escriure a la barra d’adreces el nom del teu domini.
