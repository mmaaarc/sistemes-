---
layout: default
title: "Partició i gestió de disc Windows"
---

# Partició i gestió de disc Windows

En aquest apartat veurem com afegir un disc nou en Windows.

Imagina que t'has comprat un disc, el connectes a l'ordinador i no apareix. Això és molt comú, especialment en Windows. Normalment, cal inicialitzar-lo, crear la partició i assignar-li un volum perquè es pugui utilitzar.

Afegirem el disc simulant-ho amb VirtualBox.

![Disc 1](../img/disc1.png)

En el cercador de Windows, escriu "disc" i fes clic a l'opció **Create and format hard disk partitions**.

![Disc 2](../img/disc2.png)

Aquí podem observar que ja ens apareix el nostre nou disc afegit.

![Disc 3](../img/disc3.png)

Fem clic dret sobre l’espai no assignat i després seleccionem **New Simple Volume**.

![Disc 4](../img/disc4.png)

Aquesta finestra ens permet escollir la mida de la nova partició. Podem utilitzar tot l’espai disponible o només una part si volem dividir el disc en diverses particions.

![Disc 5](../img/disc5.png)

També podem assignar una lletra de unitat al disc o, si volem, muntar-lo dins d’un directori existent en un sistema de fitxers NTFS.

![Disc 6](../img/d6.png)

En aquest pas, seleccionem el sistema de fitxers que volem utilitzar. Per a aquesta pràctica, seleccionarem **FAT32**. També podem posar-li un nom (etiqueta de volum) i seleccionar la mida de la unitat d'assignació (allocation unit size).

![Disc 7](../img/d7.png)

Un cop finalitzat, el disc ja estarà preparat per ser utilitzat!

![Disc 8](../img/d8.png)

Podem també particionar el mateix disc en dos particions diferents una amb FAT32 i l'altra amb NTFS.

![Disc 10](../img/d10.png)

Podem comprovar la configuració del disc mitjançant la línia d’ordres amb l’eina **diskpart**. Aquesta ens permet veure quants discos hi ha, les particions de cadascun, l’estat i el sistema de fitxers utilitzat, entre altres dades útils.

![Diskpart](../img/d0.png)

## Quotes de disc

Les quotes de disc són una funcionalitat molt útil per limitar l’espai que pot utilitzar cada usuari en un disc determinat. Això és especialment pràctic en entorns amb múltiples usuaris, com a escoles o empreses, per evitar que un usuari ompli tot l’espai disponible.

### Activar les polítiques de quotes

Primer de tot, hem d’habilitar les quotes de disc a través de les polítiques de Windows. Això es pot fer mitjançant l’Editor de polítiques locals o altres eines de configuració avançada.

![Quotes 0](../img/q0.png)

### Activar les quotes en el disc

Per assignar quotes de disc:

![Quotes 1](../img/q1.png)

### Configurar la quota de disc

![Quotes 2](../img/q2.png)

Un cop configurat, cada usuari tindrà restringit l’espai segons el límit que hagis establert.

## Usuaris

A Windows hi ha diferents formes d'afegir usuaris, però una de les més pràctiques i accessibles és mitjançant l'eina **netplwiz**. Aquesta utilitat permet gestionar comptes d'usuari locals de forma senzilla.

Comencem cercant **netplwiz** a la barra de cerca del menú Inici. Aquesta eina també es pot trobar com a "Advanced User Accounts Control Panel".

![Usuaris 1](../img/u1.png)

Un cop oberta la finestra, podem veure la llista d’usuaris locals. Aquí mateix es poden afegir usuaris nous mitjançant el botó **Afegeix**, però si volem un control més detallat, fem clic al botó **Advanced** per accedir a la gestió avançada.

Aquesta opció obre la consola **Local Users and Groups**, on podem veure i administrar tant usuaris com grups de forma més granular.

![Usuaris 2](../img/u2.png)

Dins la secció **Users**, si fem clic dret a l'espai buit o sobre qualezvol usuari, podem escollir **New User** per crear-ne un de nou. Aquí se'ns demana un nom d'usuari, una contrasenya (opcional), i també podem afegir una descripció i configurar opcions com obligar a canviar la contrasenya en el següent inici de sessió o impedir-ne la desactivació.

![Usuaris 3](../img/u3.png)

En aquest exemple, s’han creat dos usuaris de prova per fer pràctiques: per exemple, **Alumne1** i **Alumne2**.

![Usuaris 4](../img/u4.png)

Ara podem crear un grup nou per agrupar aquests usuaris i aplicar permisos o configuracions comunes. Per fer-ho, anem a la secció **Groups**, fem clic dret i seleccionem **New Group**. Introduïm el nom del grup (per exemple, **Pràctiques**) i podem afegir-hi usuaris fent clic a **Add** i escrivint els noms dels usuaris creats anteriorment.

Això és útil per a gestionar permisos en carpetes, programes o recursos compartits de manera col·lectiva.

![Grup 5](../img/u5.png)

Un cop creats i afegits els usuaris al grup, podem comprovar aquesta informació fent clic dret sobre un usuari i obrint la pestanya **Member of**. Aquí veurem a quins grups pertany l’usuari, com per exemple **Users**, **Administrators**, o el grup **Limitats** que acabem de crear.

![Membre de](../img/u7.png)

Per fer proves, podem iniciar sessió amb un dels nous usuaris, com ara **Alumne1**, i veure com es comporta el sistema segons les restriccions o permisos aplicats.

En aquest cas, hem copiat un fitxer gran i apareix un missatge de "Above limit" indicant que s’ha superat la quota de disc establerta per aquest usuari. Tot i que el sistema permet continuar, ens alerta del límit. Això es pot configurar perquè el sistema no permeti superar els 300MB, canviant la política de quotes en el sistema de fitxers NTFS.

![Alerta quota](../img/uu1.png)
