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
"
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
"

#### Configuraciones en VirtualBox 
* Herramientas 
  * Preferencias 
    * Detalles de la Red NAT
      - `Reenvío de puertos` 

