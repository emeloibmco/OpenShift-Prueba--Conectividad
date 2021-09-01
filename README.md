# Prueba de conectividad en OpenShift :computer::satellite:

En esta guía se realiza una prueba de conectividad de *OpenShift* y recursos exteriores al clúster, dicha prueba se lleva a cabo gracias al despliegue de una imagen de *busybox* en un Pod de *OpenShift*, que por medio de su terminal permite ejecutar comandos de verificación del estado de la conexión. Como se observa en el escenario de la prueba, la prueba de conexión se realizará con una *VSI* que se encuentra dentro de la misma subred que el clúster de *OpenShift*.

<p align="center"><img width="700" src="https://github.com/emeloibmco/OpenShift-Prueba-Conectividad/blob/main/Imagenes/diagrama.png"></p>

## Índice  📰
1. [Pre-Requisitos](#Pre-Requisitos-pencil)
2. [Ingreso a la consola de OpenShift](#Ingreso-a-la-consola-de-OpenShift-key)
3. [Creación de la imagen BusyBox en OpenShift](#Creación-de-la-imagen-BusyBox-en-OpenShift-inbox_tray)
4. [Acceso a la terminal de BusyBox](#Acceso-a-la-terminal-de-BusyBox-floppy_disk)
5. [Prueba de conectividad](#Prueba-de-conectividad-left_right_arrow)
6. [Referencias](#Referencias-mag)
7. [Autores](#Autores-black_nib)
<br />

## Pre-Requisitos :pencil:
* Contar con una cuenta en <a href="https://cloud.ibm.com/"> IBM Cloud </a>.
* Contar con un grupo de recursos específico para la implementación de los recursos.
* Contar con un cluster de OpenShift.
* Contar con una VSI for VPC para realizar la prueba de conectividad.
<br />

## Ingreso a la consola de OpenShift :key:
Ingrese a los <a href="https://cloud.ibm.com/kubernetes/clusters">clusters </a> aprovisionados y seleccione el cluster de OpenShift escogido para el ejercicio. Para ingresar a la consola, dirijase a la parte superior derecha y seleccione el icono <img width="150" src="https://github.com/emeloibmco/OpenShift-Prueba-Conectividad/blob/main/Imagenes/boton.PNG">

<br />

## Creación de la imagen BusyBox en OpenShift :inbox_tray:
1. En la consola de su clúster de OpenShift, asegurese de tener el rol como ```Developer/Desarrolador```, y seleccione la opción ```create a Project/crear un Proyecto```, a continuación ingrese un ```Nombre``` y de click en ```Crear```.
2. Una vez este creado el proyecto, en ```Topology/Topología``` seleccione la opción ```YAML``` e ingrese el siguiente YAML, el cual creará el recurso de *BusyBox* en un Pod de *OpenShift*.
```
apiVersion: v1
kind: Pod
metadata:
  name: busybox
  labels:
    app: busybox-app
spec:
  containers:
  - image: busybox
    command:
      - sleep
      - "3600"
    imagePullPolicy: IfNotPresent
    name: busybox
  restartPolicy: Always
```
3. Una vez haya ingresado el YAML, de click en ```Crear``` y espere a que la imagen sea desplegada.


<br />
<p align="center"><img width="700" src="https://github.com/emeloibmco/OpenShift-Prueba-Conectividad/blob/main/Imagenes/busybox.gif"></p>
<br />

## Acceso a la terminal de BusyBox :floppy_disk:
para acceder a la terminal de BusyBox ingrese a *OpenShift Web Cosole* y tenga en cuenta los siguientes pasos:

1. Seleccione la ventana de **Administrador** en el menú que se encuetra en la parte superior izquierda.
2. Luego de esto en este mismo menú seleccione **Workloads**>**pods**, esto lo llevara a la lista de pods disponibles.
3. seleccione el pod de BusyBox, esto lo llevara a la ventana del proyecto.
4. En esta ventana seleccione la pestaña de terminal para acceder a la terminal de BusyBox.

<br />
<p align="center"><img width="700" src="https://github.com/emeloibmco/OpenShift-Prueba-Conectividad/blob/main/Imagenes/access.gif"></p>
<br />




## Prueba de conectividad :left_right_arrow:
Una vez tenga acceso a la terminal de *busybox* podrá probar la conectividad con recursos que se encuentren afuera de *OpenShift* pero que se encuentre dentro de la misma subnet. 

Como el clúster de *OpenShift* fue creado dentro de un *VPC*, se probará su conectividad con una vsi que se encuentra de la misma *VPC*, por lo tanto tambien dentro de la misma subnet. Para probar dicha conectividad se utilizarán lo comandos ```ping``` y ```traceroute```.
<br />
<p align="center"><img width="700" src="https://github.com/emeloibmco/OpenShift-Prueba-Conectividad/blob/main/Imagenes/prueba.gif"></p>
<br />

## Referencias :mag:
* <a href="https://cloud.ibm.com/docs/cloud-infrastructure?topic=cloud-infrastructure-migrating-images-vpc"> Migración de imágenes VMDK o VHD a VPC </a>.
<br />

## Autores :black_nib:
Equipo IBM Cloud Tech Sales Colombia.






















