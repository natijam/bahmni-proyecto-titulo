# bahmni-proyecto-titulo
Proyecto de titulo 
Natalia Espinoza Carvajal
área de Informática Médica
Escuela de Ingeniería Civil Biomédica
Universidad de Valparaíso 

## Objetivo del proyecto 

El objetivo del proyecto es implementar un sistema de Información Hospitalaria de código abierto.

#### ¿Qué es un sistema de información hospitalaria? 
Dentro de un hospital existen varios tipos de sistemas de información, cada servicio en un hospital puede tener su propio sistema de información. El HIS los integra para lograr la automatización de muchas clases de transacciones y procesos.

###### Problema
No es posible  garantizar continuidad asistencial en los establecimientos de salud.  Los datos y su informacion no se mueven con el paciente, por lo tanto, el proceso asistencial se ve dañado. Aún cuando existen sistemas de información, los datos estan en silos o islas de información. Sabemos que el paciente se va a mover, queremos compartir la información 


###### Solución 
Bahmni es un sistema de información hospitalaria de código abierto que pretende satisfacer las necesidades de los entornos de bajos recursos aprovechando un conjunto de productos de código abierto existentes. Bahmni es una distribución OpenMRS. Sitio web: http://www.bahmni.org

## Requisitos técnicos

Vamos a crear una máquina virtual CentOS v7.6 utilizando VirtualBox.

- [VirtualBox](www.virtualbox.org) para Windows Host
- [CentOS-7-x84_64-DVD-1810.iso](http://ftp.iij.ad.jp/pub/linux/centos-vault/7.6.1810/isos/x86_64/CentOS-7-x86_64-DVD-1810.iso)

## Configuraciones en VirtualBox 

En VirtualBox seleccionar “Nueva”

### General
- Básico 
  - Nombre : `CentOS 7.6`
  - Tipo : `Linux`
  - Version : `Red Hat (64-bit`

### Sistema 
- Tamaño de memoria: `2048 MB`

1. Disco duro: Seleccionar "crear un disco duro virtual ahora". Next.
2. Tipo de archivo de disco duro: VDI (VirtualBox Disk Image). Next.
3. Almacenamiento en unidad de disco duro física: Reservado dinámicamente. Next
4. Ubicación del archivo y tamaño: modificar el tamaño del disco a 20 GB. Crear. 
5. La máquina está creada en VirtualBox

### Almacenamiento 

Seleccionar “Vacío” debajo de “Controlador: IDE”, seleccionar el ícono de disco a la derecha de la ventana. Click en “Seleccionar archivo de disco óptico virtual”. 

- Controlador : IDE 
  - `CentOS-7-x84_64-DVD-1810.iso`


## Configuraciones de instalación de CentOS

Al Iniciar la máquina se abrirá el asistente de instalación de CentOS 

- Idioma: `Español. Chile`
- En la sección “Sistema”, seleccionar “Destino de la instalación''.
- Aparecerá seleccionado el disco duro que creamos. Click en `Listo`. 
- Empezar instalación. 

### Durante la instalación

- Crear clave de administrador “root”. 
- Crear usuario y clave. 
  - [ ] Hacer administrador al usuario

## Finalizar instalación
- `Reiniciar` 
- License information 
  - Aceptar el acuerdo de la licencia

## Configuraciones de sistema CentOS

### Configuración de Red

#### En el terminal 
```
# para comprobar si hay conexión a internet utilizar el comando `nmcli` en el terminal
nmcli
# acceder al archivo de configuración de redes sólo visualización
cat /etc/sysconfig/network-scripts/ifcfg-enp0s3
# el comando vi permite editar el archivo
sudo vi /etc/sysconfig/network-scripts/ifcfg-enp0s3
# comando para insertar caracteres en el archivo
i 
# Cambiar `ONBOOT:no` a `ONBOOT:yes`
# Presionar la tecla “esc”
# el comando :wq guarda los cambios realizados en el archivo
:wq
sudo systemctl restart network.service
nmcli
# ahora debe mostrar enp0s3: conectado to enp0s3
# para conocer el ip de la máquina virtual
ip a
```

#### Configuraciones en VirtualBox 
* Herramientas 
  * Preferencias 
    * Detalles de la Red NAT
      - `Reenvío de puertos` 


ip anfitrion | puerto anfitrion | ip invitado | puerto invitado
--- | --- | --- | ---
ip anfitrion | 23 | ip invitado | 22
ip anfitrion | 3306 | ip invitado | 3306
ip anfitrion | 5432 | ip invitado | 5432
ip anfitrion | 80 | ip invitado | 80
ip anfitrion | 11112 | ip invitado | 11112
ip anfitrion | 443 | ip invitado | 443
ip anfitrion | 8050 | ip invitado | 8050
ip anfitrion | 8051 | ip invitado | 8051
ip anfitrion | 8052 | ip invitado | 8052
ip anfitrion | 8053 | ip invitado | 8053
ip anfitrion | 8054 | ip invitado | 8054
ip anfitrion | 8055 | ip invitado | 8055
ip anfitrion | 8057 | ip invitado | 8057
ip anfitrion | 8069 | ip invitado | 8069

## instalar bahmni

#prerequisitos.

```
sudo yum install -y https://kojipkgs.fedoraproject.org//packages/zlib/1.2.11/19.fc30/x86_64/zlib-1.2.11-19.fc30.x86_64.rpm
sudo yum install -y epel-release
```

#si no funciona, usar : sudo yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm

#instalar pip
```
sudo yum install python-pip
sudo pip install pip==v19.0

sudo pip install --upgrade pip
sudo pip install babel==v1.0 python-stdnum urllib3==1.21.1 idna==2.5 chardet==3.0.2 certifi==2017.4.17 qrcode pyserial pypdf python-chart psycogreen passlib ofxparse requests
 ```
 
#instalar paqueteria por pip
```
sudo pip install babel==v1.0 python-stdnum urllib3==1.21.1 idna==2.5 chardet==3.0.2 certifi==2017.4.17 qrcode pyserial pypdf python-chart psycogreen passlib ofxparse requests
```
#En caso que falten paquetes, pueden ser algunos de estos. 

```
sudo uninstall click
sudo pip install click==v7.0,
sudo pip install pyusbl
sudo pip install decorator==v3.4.0
sudo pip install beautifulsoup4
sudo yum install http://repo.mybahmni.org/releases/ansible-2.4.6.0-1.el7.ans.noarch.rpm
```

#instalar rpm de bahmni desde repositorio.
```
sudo yum install -y https://repo.mybahmni.org/releases/bahmni-installer-0.93-219.noarch.rpm
```
#instalar posgrest manual por RPM
```
rm -f /opt/pgdg-redhat-repo-*
cd /opt && wget https://repo.mybahmni.org/releases/pgdg-redhat-repo-42.0-23.noarch.rpm
```
#Configurar Setup.yml 
```
sudo nano /etc/bahmni-installer/setup.yml
```
#este es el contenido de setup.yml.
```
# To see the list of valid variables in Bahmni please refer to:
# https://bahmni.atlassian.net/wiki/display/BAH/List+Of+Configurable+Installation+Variables

timezone: America/Santiago
implementation_name: default
selinux_state: disabled
mysql_root_password: poner clave
mysql_old_root_password: poner clave 
openerp_url: http://poner ip :8069
# bahmni_repo_url: http://repo.mybahmni.org.s3-website-ap-southeast-1.amazonaws.com/rpm/bahmni/
bahmni_repo_url: https://repo.mybahmni.org/releases/
```
#Configurar Setup.yml y local segun necesidad
```
sudo nano /etc/bahmni-installer/local
```
#este es el contenido de local para instalacion en misma maquina full
```
localhost ansible_connection=local

[nagios-server]


[bahmni-emr]
localhost

[bahmni-emr-db]
localhost

[bahmni-emr-db-slave]

[bahmni-erp]
localhost

[bahmni-erp-db]
localhost

[bahmni-erp-db-slave]

[bahmni-lab]
localhost

[bahmni-lab-db]
localhost

[bahmni-lab-db-slave]

[bahmni-reports]
localhost

[bahmni-reports-db]
localhost

[bahmni-reports-db-slave]

[atomfeed-console]
localhost

[pacs-integration]
localhost

[pacs-integration-db]
localhost

[pacs-integration-db-slave]

[dcm4chee]
localhost

[dcm4chee-db]
localhost

[dcm4chee-db-slave]

[bahmni-event-log-service]
localhost 

[bahmni-offline]

[mysql-backup-tool]
localhost

[postgres-backup-tool]
localhost

[bahmni-backup-artifacts]
localhost

[local:children]
nagios-server
bahmni-emr
bahmni-emr-db
bahmni-emr-db-slave
bahmni-lab
bahmni-lab-db
bahmni-lab-db-slave
bahmni-erp
bahmni-erp-db
bahmni-erp-db-slave
bahmni-reports
bahmni-reports-db
bahmni-reports-db-slave
pacs-integration
pacs-integration-db
pacs-integration-db-slave
dcm4chee
dcm4chee-db
dcm4chee-db-slave
bahmni-event-log-service
bahmni-offline
atomfeed-console
mysql-backup-tool
postgres-backup-tool
bahmni-backup-artifacts
```

#cargar variables de entorno
```
echo "export BAHMNI_INVENTORY=local" >> ~/.bashrc
source ~/.bashrc
```
#correr instalador
```
sudo bahmni -i local install 
```

#backup de bahmni. total
```
bahmni -i local backup --backup_type=all --options=all
```
#restaurar bahmni

#archivos quedan en /data/ y en /home/bahmni que deben ponerse a mano en maquina destino.
```
bahmni -i local restore --restore_type=db --options=openmrs --strategy=dump   --restore_point=openmrs_dump_20170221084218.sql.gz
```
#notificaciones bahmni email
```
sudo curl -L https://github.com/Lopior/Instalador/edit/main/email-notification.properties >> /opt/openmrs/email-notification.properties
```

## Abrir Bahmni 
En el navegador de chrome, ingresar la IP local donde esta referenciado Bahmni. Se abrirá la pantalla de inicio Log in. Para acceder al programa, se debe iniciar sesión con un usuario y clave. Por defecto existe el usuario “superman” que posee todos los permisos para editar.

'usuario : superman'
'clave : Admin123'

## Cargar el diccionario de conceptos 

El diccionario de conceptos contiene todos los términos con los que trabaja el software. Los términos son variados, algunos ejemplos corresponden a anatomía, diagnósticos, síntomas, características demográficas, exámenes, etc.  
1. Iniciar sesión con el usuario superman 
2. Abrir interfaz de administracion de open mrs 'ip/openmrs/admin'
3. Abrir 'Search index'
4. hacer click en 'Rebuild Search Index'


## Internacionalización (i18n)

La internacionalización permite que la aplicación esté disponible en varios idiomas. Los pasos para configurar la internacionalización en el módulo de registro son los siguientes 

```
# Abrir el terminal 
# Abrir el directorio
cd /var/www/bahmni_config/openmrs/i18n/registration
# Conocer el contenido del directorio
ll
# Abrir el archivo locale español 
sudo nano ‘locale_es.json’
# El contenido del archivo JSON se encuentra en el github

```

## Crear usuarios 

1.	Iniciar sesión con el usuario “Superman”
2.	ingresar en la interfaz de administración de OpenMRS (ip)/openmrs/admin 
3.	Seleccionar el enlace Administrar Usuarios
4.	Clic en Agregar Usuario
5.	Click en Siguiente debajo de Crear nueva persona
6.	Agregar nombre y género de la persona
7.	Asignar un nombre de usuario y clave
8.	Asignar los roles al usuario
9.	Click en Guardar usuario
10.	Volver a la pantalla de admin 
11.	Seleccionar Administrar Proveedores
12.	Seleccionar Agregar Proveedor
13.	Rellenar el nombre de usuario con el creado anteriormente
14. Click en Guardar 


## Configurar variables globales 

1.	Iniciar sesión con el usuario “Superman”
2.	ingresar en la interfaz de administración de OpenMRS (ip)/openmrs/admin 
3.	Seleccionar el enlace Administrar propiedades globales 
4.	Modificar la lista de géneros
5.	Modificar los caracteres válidos para el nombre del paciente

## Configurar atributos de paciente en el registro de pacientes 

Las características demográficas son datos que completan la descripción de una persona, como la edad, sexo, donde vive, etc. La configuración de estos atributos se realiza en la pantalla de administración de OpenMRS. 

1.	Iniciar sesión con el usuario “superman”
2.	Ingresar en la interfaz de administración de OpenMRS (ip)/openmrs/admin 
3.	Seleccionar el enlace Administrar los tipos de atributos de persona
4.	Agregar o editar los atributos 

para que los campos de la interfaz de registro contengan la información adecuada, se debe modificar el archivo app.json del directorio /var/www/bahmni_config/openmrs/apps/registration

```
# Abrir el terminal 
# Abrir el directorio
cd /var/www/bahmni_config/openmrs/apps/registration
# Conocer el contenido del directorio
ll
# Abrir el archivo app.json
sudo nano ‘app.json’
# El contenido del archivo JSON se encuentra en el github
```

## configurar jerarquia de direcciones 

1.	Inicie sesión con el usuario “Superman”
2.	En la página de administración de OpenMRS seleccionar "Configurar jerarquía de direcciones"
3.	Cargar el archivo CSV que contiene la jerarquía de la siguiente manera 'Región -> Provincia -> Comuna'
4.	Delimiter: ;
5.	Overwrite Existing Hierarchy
6.	Clic Upload

