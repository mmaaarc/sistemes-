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
### Millores visuals i responsives

Per millorar l'aspecte de tota la pàgina recomano aplicar aquestes accions ràpides:
- Fer les imatges responsives i amb captions perquè el contingut sigui llegible en pantalles petites.
- Reduir l'amplada màxima de les imatges i centrar-les.
- Agrupar captures en una galeria amb separació i subtítols.
- Comprimir les imatges (webp/optimized) per millorar la càrrega.

Afegeix aquest estil a la capçalera del teu tema (p. ex. _includes/head.html o main.css):

<style>
/* Estils senzills per a imatges i galeria */
.responsive-img {
    display: block;
    max-width: 100%;
    height: auto;
    margin: 0.75rem auto;
    border-radius: 4px;
    box-shadow: 0 1px 4px rgba(0,0,0,0.08);
}
.gallery {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
    gap: 0.75rem;
    margin: 0.75rem 0;
}
.gallery figure {
    margin: 0;
    background: #fff;
    padding: 0.35rem;
    border-radius: 4px;
    text-align: center;
}
figcaption {
    font-size: 0.9rem;
    color: #444;
    margin-top: 0.35rem;
}
.callout {
    border-left: 4px solid #2b8cc4;
    background: #f4fbff;
    padding: 0.6rem 0.9rem;
    margin: 0.8rem 0;
    border-radius: 3px;
    color: #0b3a52;
}
</style>

Bloc d'exemple que pots reutilitzar per a cada sèrie d'imatges (canvia els noms per les teves imatges reals):

<div class="callout">
Millora ràpida: substitueix les etiquetes <img> planes per figures amb la classe <code>responsive-img</code> i/o agrupa captures en la <code>.gallery</code>.
</div>

<div class="gallery">
    <figure>
        <img class="responsive-img" src="/img/your-screenshot-1.png" alt="Descripció breu 1">
        <figcaption>Captura 1 — Pas explicat breu.</figcaption>
    </figure>
    <figure>
        <img class="responsive-img" src="/img/your-screenshot-2.png" alt="Descripció breu 2">
        <figcaption>Captura 2 — Què mostra.</figcaption>
    </figure>
    <figure>
        <img class="responsive-img" src="/img/your-screenshot-3.png" alt="Descripció breu 3">
        <figcaption>Captura 3 — Nota important.</figcaption>
    </figure>
</div>

Notes addicionals:
- Mantén el text de les captions curt i descriptiu (accessibilitat).
- Converteix les imatges a formats optimitzats i defineix amplades màximes per evitar desbordaments.
- Si vols, et genero la versió de la galeria amb els noms d'imatge ja substituïts per les teves rutes concretes.
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

- [Netplan (configuració de xarxa en Ubuntu modernes)](https://netplan.io/)
- [NetworkManager (gestió de connexions)](https://wiki.gnome.org/Projects/NetworkManager)
- [Tutorials i exemples de configuració (Ubuntu)](https://ubuntu.com/server/docs/network-configuration)

## Lliçó 6. Comandes generals i instal·lacions

- [Apt — gestió de paquets (documentació i usos comuns)](https://help.ubuntu.com/community/AptGet/Howto)
- [Snapcraft — paquets snap (instal·lació i gestió)](https://snapcraft.io/docs)
- [Comandes bàsiques de terminal (cheatsheet)](https://help.ubuntu.com/community/BasicCommands)
