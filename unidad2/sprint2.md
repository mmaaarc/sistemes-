---
layout: default
title: Sprint 2 - Título del Contenido
---

# Sprint 2

## Introducció

En aquest sprint veurem com es gestionen els usuaris, grups i permisos d'un sistema en Linux. També configurarem les polítiques de seguretat per a comptes d'usuaris i per al sistema. Instal·larem i configurarem serveis i processos essencials del sistema operatiu, crearem i administrarem sistemes de fitxers i noves particions. Implementarem un sistema de còpies de seguretat i, per últim, farem proves per comprovar el funcionament del sistema.

## Gestió de processos

- En primer lloc definirem un **procés**. Aquest és un programa en execució que inclou el seu codi, els recursos que té assignats i la seva execució. Els processos de Linux poden ser en primer o en segon pla. Els que estan en primer pla impliquen una interacció amb l'usuari, mentre que als de segon pla no es requereix aquesta interacció.
- La primera comanda que utilitzarem per llistar els processos és `pstree`. Aquesta ens mostrarà els processos actius i els seus fills (si en tenen), tot això amb forma d'arbre.

<img src="https://github.com/user-attachments/assets/215bf7cf-cf0b-448c-b8c9-eb47789faa99" alt="pstree" width="800" />

- Amb la mateixa comanda, si volem saber l'usuari corresponent i el número de procés, ho podem fer amb els paràmetres `-h` (usuari) i `-p` (procés).

<img src="https://github.com/user-attachments/assets/55c3f6c6-42f1-472d-9864-7fee2b288cf4" alt="pstree user pid" width="800" />

- A continuació veurem com **matar un procés**. Per fer-ho, serà necessari saber quin número de procés (PID) li correspon a cadascun. En el cas de matar un procés pare, tots els processos fills haurien de morir, tot i que hi ha la possibilitat que algun quedi viu; aquests s'anomenen **zombis**.
- Per matar un procés utilitzarem la següent comanda i el número de procés:

<img src="https://github.com/user-attachments/assets/7b6ac67b-5168-4905-83ec-8be42af7e21a" alt="kill command syntax" width="800" />

- Per fer la prova he utilitzat un altre terminal i m'he guardat el seu PID, per matar el procés tal com es mostra a continuació:

<img src="https://github.com/user-attachments/assets/5413851c-77ae-4224-8a0f-1adb08394575" alt="getting pid" width="800" />

<img src="https://github.com/user-attachments/assets/a48e391c-2055-4024-af45-65ac9b3cfbe8" alt="kill command execution" width="800" />

<img src="https://github.com/user-attachments/assets/67f757e9-11fb-4f03-88d3-529899d23103" alt="process killed" width="800" />

- La comanda anterior fa una "foto" instantània dels processos; aquests no canvien en temps real. Per fer una consulta en temps real utilitzarem la comanda `top`.

<img src="https://github.com/user-attachments/assets/711cb650-fa9b-4ea6-a8ff-3deebbdb4ca4" alt="top command" width="800" />

- Aquesta comanda ens dona molta informació per columnes. Vegem què vol dir cada columna:
    - **PID**: Identificador únic del procés.
    - **USER**: Usuari que inicia el procés.
    - **%CPU**: Percentatge d'ús del processador.
    - **%MEM**: Percentatge d'ús de la memòria RAM.
    - **COMMAND**: Nom de la comanda o programa.

<img src="https://github.com/user-attachments/assets/7672e4fb-8d6b-4829-9dff-99ce37fa1c0b" alt="top columns" width="800" />

- En cas d'obrir un nou procés (ex: navegador) aquest ens apareixerà a la llista.

<img src="https://github.com/user-attachments/assets/65274143-a389-4eb5-ba04-5cf391a505d0" alt="new process in top" width="800" />

- La prioritat no es pot modificar directament, però amb el **NI (nice)** sí que es pot canviar. Contra més baix és el número, més prioritat té. Això es pot fer amb la següent comanda. Cal dir que caldria fer-ho des del `root`, ja que ens atorga més privilegis.

```bash
renice -n -nºprioritat -p PID
```

<img src="https://github.com/user-attachments/assets/ccda0c72-03a6-4d4f-92ec-ca06d16cf5e2" alt="renice command" width="800" />

<img src="https://github.com/user-attachments/assets/258b10bc-ef08-45f9-a89b-999f0a9390cc" alt="renice result" width="800" />

- Aquesta comanda serveix per a moments determinats; la prioritat per `renice` no és permanent.
- Seguidament també podem utilitzar la comanda `ps aux`, que ens dona una informació similar però amb diferents paràmetres que veurem a continuació:
    - **USER**: Usuari que ha iniciat el procés.
    - **PID**: Identificador únic del procés.
    - **%CPU i %MEM**: Percentatge de CPU i memòria RAM utilitzats pel procés.
    - **VSZ**: Memòria virtual total utilitzada pel procés.
    - **RSS**: Memòria física utilitzada pel procés.
    - **TTY**: Terminal associat al procés (`?` si no en té).
    - **STAT**: Estat del procés.
        - `R`: Executant-se (Running).
        - `S`: Inactiu (Sleeping).
        - `T`: Pausat (Stopped).
        - `Z`: Procés zombi.
        - `I`: Inactiu o sense consumir recursos.
        - `<`: Alta prioritat de CPU.
        - `s`: Líder de sessió.
        - `l`: Multithread.
        - `+`: Associat al terminal en primer pla.

```bash
ps aux
```

<img src="https://github.com/user-attachments/assets/d9192ceb-47c4-456c-8a71-dedf9b30afb8" alt="ps aux" width="800" />

- Amb el `ps` podem fer vàries combinacions per mostrar informació en concret. A continuació veurem quines són i què fan:

```bash
ps -e
```
Mostra tots els processos del sistema amb una sintaxi estàndard.

```bash
ps -ejH
```
Mostra un arbre de processos.

```bash
ps -eLf
```
Mostra la informació dels fils (threads).

```bash
ps -eM
```
Mostra informació de seguretat.

```bash
ps -U root
```
Mostra tots els processos de l'usuari root.

- A continuació veurem què són els processos en **segon pla** i com passar processos a aquest estat. Com hem dit abans, amb `kill -9` matem un procés, amb `Ctrl+C` l'aturem, i amb `Ctrl+Z` el passaríem a segon pla (pausat). (Nota: segons el tipus de procés que aturem, si aquest va per terminal potser no se'ns mostra en segon pla).
- La comanda per veure els processos en segon pla és:

```bash
jobs
```

<img src="https://github.com/user-attachments/assets/f8cdc2e2-ac60-4a5a-8ff8-5d847f3548a7" alt="jobs command" width="800" />

- Un cop tenim aquest procés localitzat, si no volem matar-lo sinó que el volem enviar al primer pla, podem utilitzar la següent comanda:

```bash
fg %nº
```

<img src="https://github.com/user-attachments/assets/f2388788-aa72-428c-aaa9-35fdd035eacf" alt="fg command" width="800" />

<img src="https://github.com/user-attachments/assets/f88e3e71-4499-423f-a64d-7796ed0cbfee" alt="process foreground" width="800" />

<img src="https://github.com/user-attachments/assets/73352b91-7548-4322-8691-4d389e29810e" alt="process foreground output" width="800" />

- En cas de voler fer el procés invers i enviar un procés al segon pla podem utilitzar:

```bash
bg %nº
```

- En algun cas especial, potser voldrem executar algun procés directament en segon pla; es pot fer de la següent forma:

```bash
nomproces &
```

- A l'hora de consultar processos amb `top` hem vist que és una eina en viu i que els processos es van movent, cosa que a vegades pot fer complicat llegir-ho. En cas de voler evitar això i consultar només el PID d'un procés en concret, podem fer servir `pidof`:

<img src="https://github.com/user-attachments/assets/09c1efd8-b3ac-4c23-8230-b9c21597a698" alt="pidof command" width="800" />

- Una altra forma de fer-ho podria ser utilitzant comandes anteriors i afegir un `grep`, però en algunes opcions com el `ps aux` pot quedar una mica confús. Personalment, recomano `pstree` ja que així veurem també els processos fills.

<img src="https://github.com/user-attachments/assets/110e7f30-bb99-4468-a3b9-28c2fef3cb92" alt="ps grep" width="800" />

- Per acabar, si en algun moment volem utilitzar algun script o procés i que aquest tingui una prioritat predeterminada per nosaltres, es pot fer amb `nice`.

<img src="https://github.com/user-attachments/assets/e37c94ae-383d-4593-b052-e703a48f83d3" alt="nice command" width="800" />

- Amb un `top` podem comprovar si ha funcionat correctament.

<img src="https://github.com/user-attachments/assets/10a41317-8f8d-4043-84c2-25179f32ca07" alt="checking nice with top" width="800" />

---

## Gestió d'usuaris, grups i permisos

És important que al nostre sistema tinguem diferents usuaris i que aquests tinguin diferents característiques, i que els puguem incloure en grups per classificar-los. A més a més, també ens interessarà poder modificar-los, eliminar-los i bloquejar-los al nostre gust. Tot això i més ho veurem a continuació.

### Comandes de terminal i accessos als directoris

Per accedir al terminal normalment ho farem amb `Ctrl + Alt + T`, així obrim el pseudo-terminal. El terminal com a tal l'obrirem amb `CtrlDret + F3` (un terminal TTY). Un pseudo-terminal és com un emulador on les comandes que posem són interpretades per algun arxiu al qual fan referència i aquest fa els procediments; en canvi, amb un terminal "real" estem en contacte més directe amb el sistema.

- En primer lloc, veurem un document que actua com un registre de tots els comptes d'usuaris presents al sistema: `/etc/passwd`. Inclou dades com el nom del compte, l'identificador d'usuari (UID), el directori personal i el shell configurat per defecte. Es tracta d'un fitxer públic, cosa que permet que qualsevol pugui consultar qui són els usuaris del sistema.

<img src="https://github.com/user-attachments/assets/d23bb83f-8d3f-4d99-bda1-853774c7fe34" alt="users file" width="800" />

- A continuació podem veure els grups dels usuaris i l'identificador de qui és el seu administrador.

<img src="https://github.com/user-attachments/assets/2df9ea67-4b6e-4a2d-96e4-44d365e7fc70" alt="groups file" width="800" />

- En l'arxiu `/etc/shadow` es guarda la informació relacionada amb les contrasenyes dels comptes d'usuari. Cada registre fa referència a un usuari i inclou la seva contrasenya codificada. Si apareix el símbol `!`, indica que el compte està deshabilitat i l'usuari no té permís per accedir al sistema.

<img src="https://github.com/user-attachments/assets/dd4e8d09-8d07-4ac0-883d-03e823be34b4" alt="shadow file" width="800" />

- Per últim, l'arxiu `/etc/gshadow` és comparable a `/etc/group`, però ofereix detalls extres sobre els grups. En aquest lloc es pot identificar qui són els administradors de cada grup. Resulta pràctic per controlar els permisos i gestionar els privilegis d'accés dels diferents grups d'usuaris.

<img src="https://github.com/user-attachments/assets/b2d4bbc8-22f6-43f2-b71a-cc7721e171af" alt="gshadow file" width="800" />

### Creació d'usuaris

Per crear usuaris tenim diverses formes de fer-ho. El més important és tenir clar que amb certes comandes no es creen els directoris personals automàticament.

- En primer lloc utilitzarem la següent comanda, que crearà un usuari, però fins que no iniciem sessió amb ell no es crearan els directoris. Aquesta és la forma més senzilla, ja que ve pautada pel mateix sistema operatiu.

<img src="https://github.com/user-attachments/assets/4b36b735-3c79-4881-83b8-e884a2fa1aca" alt="create user simple" width="800" />

- Per crear un nou compte d'usuari amb més control, farem servir la comanda `useradd`. Aquesta comanda ens permetrà afegir usuaris al sistema amb diversos paràmetres:
    - `-m`: Indica que es generarà automàticament un directori personal per a l'usuari.
    - `-s /bin/bash`: Defineix el shell per defecte de l'usuari.
    - `-d /home/alumne2`: Especifica el directori inicial de l'usuari.
    - `alumne2`: Correspon al nom de l'usuari que estem creant.
    - `&& passwd alumne2`: Aquesta comanda s’utilitza per assignar o modificar la contrasenya de l’usuari.

<img src="https://github.com/user-attachments/assets/eb070f06-729d-45f2-a18c-d229337cd1c1" alt="useradd command" width="800" />

- Si no utilitzem l'opció `-m` per als directoris, els podem afegir manualment de la següent manera:

<img src="https://github.com/user-attachments/assets/548e1a70-b290-4279-9496-3e16c9a4950c" alt="manual home dir" width="800" />

- Si volem canviar el nom de l'usuari podem utilitzar la comanda `usermod`. En el cas següent, canviarem el nom `porva2` a `prova2`:

<img src="https://github.com/user-attachments/assets/7385f45b-dce6-4120-87d6-0142f5cdc274" alt="rename user 1" width="800" />
<img src="https://github.com/user-attachments/assets/d52d9e61-83e2-4345-8d5e-d31d20ade4db" alt="rename user 2" width="800" />

- En cas de voler eliminar l'accés a un usuari, ho podem fer bloquejant-lo. Una forma de comprovar que s'ha bloquejat correctament és entrar al fitxer `passwd` (o `shadow`) i veure que la contrasenya té un signe d'exclamació `!` al davant.

<img src="https://github.com/user-attachments/assets/f12ad2ef-0b87-4053-8e79-29517ddb6f54" alt="lock user" width="800" />
<img src="https://github.com/user-attachments/assets/9d5bd325-2aba-4974-9407-0937df9fa434" alt="locked user check" width="800" />

- Si tenim un usuari bloquejat i el volem recuperar, utilitzarem la comanda de desbloqueig. Com a comprovació, veurem que ja no té l'exclamació.

<img src="https://github.com/user-attachments/assets/4c152dee-42ab-467a-a932-754886469ec7" alt="unlock user" width="800" />

- Si realment el que volem és eliminar l'usuari de forma més permanent:

```bash
deluser usuari
```

<img src="https://github.com/user-attachments/assets/039668ec-68df-4efd-b48b-f8e03669bced" alt="deluser command" width="800" />
<img src="https://github.com/user-attachments/assets/6a2ecf2d-7c39-48f3-abe0-6f591e891579" alt="deluser check" width="800" />

- En cas de voler consultar algun tipus d'informació sobre algun usuari, podem fer-ho així:

<img src="https://github.com/user-attachments/assets/4c6cca96-9895-46a4-bb4c-c9846fb70c4a" alt="id user" width="800" />

- Un cop vist el funcionament a través del terminal, podrem observar com es fa per la interfície gràfica d'Ubuntu. Dins de la configuració de sistema hem d'entrar a l'apartat **Usuaris**.

<img src="https://github.com/user-attachments/assets/911eb5d0-b1ba-488a-bb72-7dcd6f7270e4" alt="gui users 1" width="800" />
<img src="https://github.com/user-attachments/assets/cc0d32df-f2f5-4fce-98ab-e503955f2b41" alt="gui users 2" width="800" />
<img src="https://github.com/user-attachments/assets/51857bcc-5d9b-401e-9ed7-5f68f128d39d" alt="gui users 3" width="800" />
<img src="https://github.com/user-attachments/assets/2ac38f68-b752-496a-a097-ab6b6607e4e8" alt="gui users 4" width="800" />
<img src="https://github.com/user-attachments/assets/a600484b-9d25-45df-9367-4dc3312a565e" alt="gui users 5" width="800" />

### Creació de grups

- En aquest apartat veurem com funcionen els grups d'usuaris. Important dir que quan es crea un usuari normalment també es crea un grup amb el mateix nom.
- Per crear un grup nou ho podem fer amb una senzilla comanda:

<img src="https://github.com/user-attachments/assets/a1fcd813-6cff-4a72-844c-f535f54a7a88" alt="addgroup" width="800" />
<img src="https://github.com/user-attachments/assets/418a4288-c902-4f15-9c3e-e82a977bb3aa" alt="check group" width="800" />

- Si volem afegir un usuari a un grup existent:

<img src="https://github.com/user-attachments/assets/9c174a94-bb9f-4368-a66d-aa43f65a063a" alt="adduser to group" width="800" />
<img src="https://github.com/user-attachments/assets/26e761d3-e20c-4bd3-b80b-6a1927af0fd1" alt="verify group members" width="800" />

- Per fer administrador d'un grup a un usuari, ho podem fer així. Dins de l'arxiu `gshadow` podem veure els usuaris i administradors; per reconèixer-los, veurem la posició que tenen entre els `:`.

<img src="https://github.com/user-attachments/assets/376246e4-4a77-4e95-ac9a-333ba3222e07" alt="gpasswd" width="800" />
<img src="https://github.com/user-attachments/assets/25c71f85-31b9-4c92-ba80-bf959b2437e3" alt="gshadow check" width="800" />

- Un dels problemes potencials és que, quan afegim usuaris a grups amb certes comandes, es poden treure del grup on estaven. Per evitar-ho, utilitzarem `usermod -aG`. Com comprovarem, l'usuari `alumne2` forma part dels dos grups d'asix i és administrador del primer.

<img src="https://github.com/user-attachments/assets/943f8804-056c-4c79-b2fe-3aad995b19e6" alt="usermod append" width="800" />
<img src="https://github.com/user-attachments/assets/fe556799-ad48-448c-8c02-c148596aa8b8" alt="groups check" width="800" />

- Per eliminar un usuari d'un grup (en aquest cas traiem `alumne2` de `asix1`):

<img src="https://github.com/user-attachments/assets/1e646ff4-81c1-40db-a053-abd0baec0ac4" alt="gpasswd delete" width="800" />
<img src="https://github.com/user-attachments/assets/a2107e97-f40f-4b8f-a119-08f4edfd1877" alt="group check after delete" width="800" />

- L'anterior acció també es pot fer amb `deluser`:

<img src="https://github.com/user-attachments/assets/1d9f44ea-686f-46c9-966b-84cbf6407f56" alt="deluser from group" width="800" />

- Per canviar el grup principal d'un usuari:

```bash
usermod -g grup usuari
```

- En cas de voler canviar el nom d'algun grup:

<img src="https://github.com/user-attachments/assets/63288eeb-bb01-4128-829e-d68fda365738" alt="groupmod rename" width="800" />
<img src="https://github.com/user-attachments/assets/ed9761c4-a05b-4b68-b03f-0b4463e482b6" alt="check rename" width="800" />

---

## Gestió de permisos

En un sistema multiusuari on volem que diferents usuaris tinguin certs permisos però no els mateixos, és important fer una bona gestió. Hi ha vàries maneres de gestionar-ho.

### Permisos estàndards

- Els permisos estàndards són una sèrie de permisos bàsics que es poden donar a usuaris i grups. Els grups poden tenir diferents permisos respecte als usuaris.
- Podem observar els permisos amb `ls -l`. El primer nom és l'usuari propietari i el segon és el grup propietari.

<img src="https://github.com/user-attachments/assets/fb0e3317-4a01-4e0b-9b6e-7be37e86b2ef" alt="ls permissions" width="800" />

- **Interpretació**:
    - `d`: Directori.
    - `rwx` (Usuari): Lectura, escriptura, execució.
    - `r-x` (Grup): Lectura i execució, sense escriptura.
    - `r-x` (Altres): Lectura i execució, sense escriptura.
- **Canviar propietari (chown)**:
  D'aquesta manera faig propietari de la carpeta `cire` a l'usuari `cire`.

<img src="https://github.com/user-attachments/assets/6d457e01-774c-4da9-89dd-d6c2c06ada47" alt="chown user" width="800" />
<img src="https://github.com/user-attachments/assets/8bd4d361-e6b3-4b75-a5f4-62f26dd7af74" alt="chown check" width="800" />

- **Canviar grup (chgrp)**:
  Amb aquesta opció canvio el grup de la carpeta `cire` al grup `cire`.

<img src="https://github.com/user-attachments/assets/2e4028b2-ab6f-40bf-acba-83e6882e7b2c" alt="chgrp" width="800" />
<img src="https://github.com/user-attachments/assets/c42be974-277f-4651-9872-85601f3e041e" alt="chgrp check" width="800" />

- **Canviar-ho tot alhora (chown usuari:grup)**:
  També podem canviar l'usuari i el grup simultàniament, així com fer-ho recursivament (`-R`).

<img src="https://github.com/user-attachments/assets/022cf7fe-20ec-4ff3-b2a3-ef4b1325db11" alt="chown recursive" width="800" />

### Permisos especials

#### Sticky Bit
L'Sticky Bit és un permís d'accés per a fitxers i directoris. Quan l'apliquem, l'únic usuari que pot eliminar o moure un fitxer dins d'un directori és el seu propietari (o root), encara que altres usuaris tinguin permís d'escriptura al directori.
- S'aplica amb `chmod +t` o `chmod 1777`.

<img src="https://github.com/user-attachments/assets/9934016a-f588-40f1-b4ab-61ec11cfa7ef" alt="sticky bit" width="800" />

A l'hora de veure els permisos ens sortirà una `t` al final.

<img src="https://github.com/user-attachments/assets/39e56fd0-d23b-4c20-aa08-c86c4a321533" alt="sticky bit check" width="800" />

Per eliminar-lo: `chmod -t`.

<img src="https://github.com/user-attachments/assets/b06250ea-2e85-42c4-acb7-3dbd5e59f599" alt="remove sticky bit" width="800" />

#### SGID (Set Group ID)
El SGID és un permís relacionat amb els grups. En directoris, fa que qualsevol arxiu creat a dins hereti el grup del directori, i no el grup principal de l'usuari que el crea.

<img src="https://github.com/user-attachments/assets/820fd185-5e48-465e-b3cc-f370fc4fadf6" alt="sgid" width="800" />

Si ara des d'un altre usuari (com `marc`) creo un arxiu dins, aquest agafarà el grup del directori.

<img src="https://github.com/user-attachments/assets/a0ab8f27-496a-439b-b582-6c80511b0d6a" alt="sgid check" width="800" />

#### SUID (Set User ID)
Permet que un arxiu s'executi amb els permisos del propietari del fitxer, independentment de l'usuari que l'executi. A diferència del SGID i Sticky, no sol aplicar-se a scripts per seguretat.

```bash
chmod u+s fitxer
```

### Llistes de control d'accés (ACLs)

Les ACLs ens permeten configurar accessos més granulars que els permisos estàndard (rwx). Per utilitzar-les necessitem el paquet `acl`.

- Per **configurar una ACL** (`setfacl`):

<img src="https://github.com/user-attachments/assets/a16dc818-9df5-46ad-babb-d2da491e75fb" alt="setfacl" width="800" />

- Per **veure les ACLs** (`getfacl`):

<img src="https://github.com/user-attachments/assets/8f2cd0b6-43f4-4d02-8275-e900b98231c5" alt="getfacl" width="800" />

- Exemple: treure permisos a l'usuari `segon`:

<img src="https://github.com/user-attachments/assets/04bd1954-a6ef-4227-8a75-ad77ada5a338" alt="setfacl zero" width="800" />

<img src="https://github.com/user-attachments/assets/a36759e9-bca4-41d9-b9ab-4ca1da3709c4" alt="getfacl zero" width="800" />

<img src="https://github.com/user-attachments/assets/4aa618c9-019e-4d4d-9c17-4f07757bf81d" alt="acl check" width="800" />

### Umask

Umask determina els permisos per defecte dels nous arxius i directoris. El valor és el que es **resta** als permisos màxims (666 per fitxers, 777 per directoris).

- Exemple amb umask 027 (777-027 = 750 / 666-027 = 640):

<img src="https://github.com/user-attachments/assets/c88fbc7e-bd1c-442e-8c2f-2d743f394e9c" alt="umask set" width="800" />
<img src="https://github.com/user-attachments/assets/f7809532-7d7c-48ec-87f3-a01c66ccc16a" alt="touch umask" width="800" />
<img src="https://github.com/user-attachments/assets/9efd005a-516a-4286-9567-fc6bd16f7d19" alt="check umask perm" width="800" />

- Per fer-ho permanent `~/.bashrc`:

<img src="https://github.com/user-attachments/assets/60283044-992a-458e-80a0-8cac398ffd8d" alt="umask permanent" width="800" />

---

## Sistemes de fitxers i particions

### Estructura de la informació

L'estructura de la informació la podem dividir en física (disc sòlid o mecànic) i lògica (GPT o MBR).

<img src="https://github.com/user-attachments/assets/7a4d382e-6ea4-46e0-83fd-2e06b3c999d6" alt="partitions info" width="800" />

- Els discs estan dividits en blocs i sectors. El sector és la unitat mínima física (per defecte 512 bytes). El sistema operatiu treballa en blocs (unitat lògica). La mida del bloc es pot canviar en formatar la partició.

<img src="https://github.com/user-attachments/assets/2d120054-219d-43ec-84d7-ef46f01d9e97" alt="block sizes" width="800" />
<img src="https://github.com/user-attachments/assets/9ebdf43f-0be8-4719-baf2-1d72cffc8429" alt="blockdev info" width="800" />

- Per saber informació de fitxers i particions (`lsblk -f`):

<img src="https://github.com/user-attachments/assets/021db590-85fc-4be2-bf7e-33e25b59e410" alt="lsblk" width="800" />

#### Fragmentació
- **Fragmentació interna**: Espai desaprofitat dins dels blocs perquè els fitxers no els omplen del tot. Blocs petits redueixen això però poden augmentar la fragmentació externa.
- **Fragmentació externa**: Arxius guardats en blocs no contigus, reduint el rendiment.

#### Tipus de formateig
1. **Ràpid**: Elimina el sistema de fitxers, ignora blocs defectuosos.
2. **Nivell mitjà**: Elimina el sistema de fitxers, detecta blocs defectuosos (sense reparar).
3. **Nivell baix**: Esborra tot i intenta reparar sectors.

<img src="https://github.com/user-attachments/assets/686403c1-68e1-4e01-87c8-3e08954b2804" alt="format commands" width="800" />
<img src="https://github.com/user-attachments/assets/653001d8-3033-4340-b34a-db3d3bcb4b35" alt="fsck check" width="800" />

### Particions

#### Creació i formateig
- Entrem al disc amb `fdisk /dev/sdb`.
- Creem particions (`n`), definim sectors i tipus.

<img src="https://github.com/user-attachments/assets/bb2bac5b-cc6b-4121-8d6c-c16781271314" alt="fdisk steps" width="800" />

- Comprovem amb `fdisk -l`.

<img src="https://github.com/user-attachments/assets/9416e5f6-7e29-4be0-9b6f-385137338067" alt="fdisk list" width="800" />

- Formatat amb `mkfs`:

<img src="https://github.com/user-attachments/assets/845d4fcd-d452-4a70-9325-21ab0abe34c6" alt="mkfs" width="800" />

#### Muntatge
- **Temporal**: `mount /dev/sdb1 /punt/muntatge`. Els fitxers anteriors al punt de muntatge s'oculten fins que es desmunti.

<img src="https://github.com/user-attachments/assets/82590cb4-ff22-451b-8502-0ec22ea4a0e5" alt="mount step 1" width="800" />
<img src="https://github.com/user-attachments/assets/d5138754-3d01-442a-8096-ef68bc61dfe7" alt="mount lost found" width="800" />
<img src="https://github.com/user-attachments/assets/a4fce79b-0cf1-4fa1-91a4-ce0a28beef7f" alt="mount check file" width="800" />

- **Permanent**: `/etc/fstab`.

<img src="https://github.com/user-attachments/assets/8092c66d-1cd5-491d-8521-da5af88b893d" alt="fstab" width="800" />

---

## Còpia de seguretat i automatització de tasques

### Teoria
- **Completa**: Còpia de tot. Avantatge: fàcil restaurar. Inconvenient: ocupa molt i és lenta.
- **Diferencial**: Còpia tot el que ha canviat des de l'última completa. Restauració: Última completa + última diferencial.
- **Incremental**: Còpia el que ha canviat des de l'última còpia (sigui quina sigui). Restauració: Completa + totes les incrementals.

### Programes i Comandes
- **cp**: Còpia simple local.
- **rsync**: Còpia intel·ligent, només fitxers modificats, suporta xarxa (SSH).
- **dd**: Clonació bit a bit (particions/discs).

### Automatització amb Cron i Anacron
- **Cron**: Per a servidors o màquines sempre enceses. Executa tasques a hores exactes.
- **Anacron**: Per a desktops/portàtils. Executa tasques pendents si l'ordinador estava apagat.

#### Configuració Cron
- `crontab -e -u usuari`: Tasques d'usuari.
- `/etc/crontab`: Sistema.

<img src="https://github.com/user-attachments/assets/82bcf1d7-8807-435a-80cf-0dc5555e44af" alt="anacrontab file" width="800" />

#### Exemple Script Backup

1. Crear script `.sh`.

<img src="https://github.com/user-attachments/assets/ec50567a-2a45-4adb-bfed-80898f407cdf" alt="create directories" width="800" />
<img src="https://github.com/user-attachments/assets/754f35db-4566-4525-9ead-2b81de9b0692" alt="backup script" width="800" />

2. Afegir a crontab.

<img src="https://github.com/user-attachments/assets/7185d014-cb93-4e38-8231-d501ce504023" alt="crontab edit" width="800" />
<img src="https://github.com/user-attachments/assets/a11cac4c-5fe6-48aa-9dc6-83083e17f091" alt="cron result" width="800" />

3. Moure a `cron.daily` per Anacron.

<img src="https://github.com/user-attachments/assets/0876464b-819f-468e-b195-167051cc11a3" alt="move to daily" width="800" />
<img src="https://github.com/user-attachments/assets/6e232b62-965f-4da1-af16-403107473348" alt="check daily" width="800" />
<img src="https://github.com/user-attachments/assets/74d51513-5033-42e3-8f93-5f61e6fb8dba" alt="check daily 2" width="800" />

4. Configuració Anacron `/etc/anacrontab`.

<img src="https://github.com/user-attachments/assets/83c01aa8-d993-42c9-a292-a3eab5ec1bf1" alt="anacron stamp" width="800" />
<img src="https://github.com/user-attachments/assets/9c9edaec-2431-4d89-aaba-dee9757cf6c6" alt="anacrontab config" width="800" />
<img src="https://github.com/user-attachments/assets/c0003167-3596-4781-927b-2bdad20c237a" alt="anacron result 1" width="800" />
<img src="https://github.com/user-attachments/assets/5fff0aa2-2eb5-4b04-87bb-71f619a6c6bf" alt="anacron result 2" width="800" />

---

## Quotes de disc

Les quotes de disc limiten l'ús d'emmagatzematge per usuari o grup.

1. Instal·lar `quota`.
   ```bash
   sudo apt update
   sudo apt install quota
   ```
   <img src="https://github.com/user-attachments/assets/49d81f4f-1df8-459c-9ac9-e22fc129018d" alt="install quota" width="800" />

2. Configurar `/etc/fstab` afegint `usrquota` i `grpquota`.
3. Activar quotes (remount i quotaon).
   ```bash
   quotacheck -cug /mnt/dades
   quotaon /mnt/dades
   ```
   <img src="https://github.com/user-attachments/assets/4a25555f-4753-4b9d-b8b7-5944d06f2b10" alt="quota commands" width="800" />

4. Editar quota d'usuari (`edquota -u usuari5`).
   <img src="https://github.com/user-attachments/assets/c5c907f0-622f-4674-954c-22d7fc917acd" alt="edquota" width="800" />
   - **soft**: Límit advertència.
   - **hard**: Límit estricte.

5. Prova d'emplenat amb `dd` (crear fitxer gran).
   ```bash
   dd if=/dev/zero of=test bs=1K count=800
   ```

6. Comprovar estat:
   ```bash
   repquota /dev/sdc1
   ```
   <img src="https://github.com/user-attachments/assets/4deb80a2-1845-45dd-833f-4a65b6ffe9c8" alt="repquota" width="800" />

   <img src="https://github.com/user-attachments/assets/fc1f9025-6f2c-4107-90b9-b5a569355a84" alt="quota exceeded" width="800" />

   <img src="https://github.com/user-attachments/assets/d246d18b-05d8-43e6-b7be-33a5944b4c19" alt="quota user check" width="800" />

7. Dies de gràcia (`edquota -t`).
   <img src="https://github.com/user-attachments/assets/8268577f-f410-4178-bb8c-3a54312f8aa8" alt="quota grace" width="800" />
