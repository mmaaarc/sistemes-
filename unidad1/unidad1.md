---
layout: default
title: "sprint 1"
---

## Lliçó 1. Virtualització i instal·lació del sistema operatiu Ubuntu
En aquest apartat explicare i realitzare una instal·lació del sistema Ubuntu Desktop on posteriorment instal·lare un Windows 10 com a dual.

L'instal·lació la fare apartir d'una màquina virtual al VirtualBox.
Primer li poso un nom i la iso que ens permetra poder instal·lar l'Ubuntu.

<img src="../img/primer.png" alt="Captura de la instal·lació d'Ubuntu" width="720">

També li assigno la memoria amb 6144MB tindrem prou.

<img src="../img/memoria.png">

I finalment li he assignat un disc de 80GB ja que em te que sibrar espai per poder instal·lar el Windows posteriorment
Per tant 25GB son per Ubuntu Desktop.
<img src="../img/disc.png">

Ara ja puc iniciar la màquina i començar la instal·lació.
<img src="../img/instalar.png">

Seguim amb l'instal·lació.
<img src="../img/install.png">

En aquesta part selecciono la segona opció on puc configurar les particions.

<img src="../img/particions.png">

Ara li assigno l'arrel del sistema que és la particion més gran que necessita més espai.

<img src="../img/30.png">

Finalment el swap que és important si falla la memoria o no es suficient.

<img src="../img/swap.png">

I així queda la taula de particions.

<img src="../img/total.png">

I configuro els últims paràmetres.

<img src="../img/fin">

I començara la instal·lació.

<img src="../img/fin.png">

Un cop instl·lat apagare la màquina i inserire la iso del Windows pero poder instal·larlo.

<img src="../img/win.png">

Ara torno a obrir la màquina prenent f12 per entrar al mode arranc.
<img src="../img/dual.png">

I cliquem a la c amb CD-ROOM que és la unitat física que hem inserit del Windows.

I ara ja podre instal·lar el Windows.

<img src="../img/win1.png">

En aquest pas selecciono instal·lar Windows avançat per configurar les meves propies particions.

<img src="../img/pas.png">

I com podem veure em surt que ja tinc Ubuntu instal·lat i l'espai del disc guardat per poder instal·lar Ubuntu.

<img src="../img/parti.png">

I començara la instal·lació.

<img src="../img/on.png">

I esperare a que inicie el windows.

<img src="../img/inici.png">

I ara configuro els paràmetres bàsics.

<img src="../img/basic.png">

<img src="../img/fet.png">

## Lliçó 2. Llicenciament

- [Llicències GNU i llibertat de programari (FSF)](https://www.gnu.org/licenses/licenses.html)
- [Open Source Initiative — Llicències OSS](https://opensource.org/licenses)
- [Informació sobre llicències i codi a Ubuntu](https://ubuntu.com/about/ubuntu-licences)

## Lliçó 3. Gestors d'arrencada per a instal·lacions duals

- [Manual de GRUB (GNU GRUB)](https://www.gnu.org/software/grub/manual/)
- [rEFInd (gestor d'arrencada alternatiu)](https://www.rodsbooks.com/refind/)
- [Guia pràctica per a dual-boot amb Ubuntu](https://help.ubuntu.com/community/UbuntuDualBoot)

## Lliçó 4. Punts de restauració

- [Timeshift — eines de snapshots per a Linux](https://github.com/teejee2008/timeshift)
- [Snapshots amb Btrfs (documentació)](https://btrfs.wiki.kernel.org/index.php/SNAPSHOTS)
- [Estratègies de còpia de seguretat i restauració en Ubuntu](https://ubuntu.com/server/docs/backup-restore)

## Lliçó 5. Configuració de la xarxa

## MODE GRÀFIC 

En aquest apartat configurare una IP manual amb sortida a internet

Per configurar la xarxa en primera instancia podem veure la configuració a través dels paràmetres a l'opció de xarxa. Des d'aquest punt entrem a les opcions del cablejat per comprovar quina IP tenim i amb el mode manual la podem canviar al nostre gust.
Com podem veure tinc una interfície connectada.

<img width="633" height="183" alt="image" src="https://github.com/user-attachments/assets/426f8bbd-45e7-40c9-bd04-95e309fd6782" />

I si accedim podrem veure que té una IP assignada.

<img width="749" height="388" alt="image" src="https://github.com/user-attachments/assets/c84b4a21-251e-4102-a2c9-d6877103ee8a" />

Aquesta IP ens la dona VirtualBox, ja que tinc posada la NAT en aquesta interfície.

<img width="749" height="388" alt="image" src="https://github.com/user-attachments/assets/3e2121f6-48b9-4b48-bc0b-cdf26d6cbdcd" />

I ara per fer la prova li he posat una IP manualment 192.168.10.2 i la IP 8.8.8.8 per la resolució de domini cap a internet

<img width="810" height="521" alt="image" src="https://github.com/user-attachments/assets/7d82ea01-b9ec-4598-b5ad-b929795a03c9" />

I amb la comanda ip a puc comprovar que s'han aplicat els canvis.

<img width="816" height="420" alt="image" src="https://github.com/user-attachments/assets/5ca41a68-098b-4cec-b94e-ae7a6dc05521" />

## MODE TERMINAL

Desde el fitxer /etc/netplan podem modificar la configuració de xarxa per terminal.

<img width="767" height="46" alt="image" src="https://github.com/user-attachments/assets/218a6fb6-7fb2-4a08-a8fb-57955fac97a1" />

<img width="816" height="320" alt="image" src="https://github.com/user-attachments/assets/22cb737f-cff0-4ac0-a151-829300ec5f74" />

Finalment li dono permisos i faig el netplan apply.
<img width="662" height="203" alt="image" src="https://github.com/user-attachments/assets/3bf0106e-8848-4c9f-ac29-6f4eaee312c5" />

I amb la comanda ip a comprovo que s'han aplicat els canvis.

<img width="1041" height="326" alt="image" src="https://github.com/user-attachments/assets/649a020c-3b89-44a0-bb68-b741d564c5e8" />




a
## Lliçó 6. Comandes generals i instal·lacions

- [Apt — gestió de paquets (documentació i usos comuns)](https://help.ubuntu.com/community/AptGet/Howto)
- [Snapcraft — paquets snap (instal·lació i gestió)](https://snapcraft.io/docs)
- [Comandes bàsiques de terminal (cheatsheet)](https://help.ubuntu.com/community/BasicCommands)
