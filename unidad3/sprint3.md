En primer lloc he creat la màquina servidor on instal·lare el ldap.

Aquesta màquina la configurare amb Xarxa NAT.

<img width="872" height="543" alt="image" src="https://github.com/user-attachments/assets/33a9bdb6-11da-4d0e-b1c0-d5fa2ca4c171" />

I aquesta és la IP de la màquina.

<img width="733" height="290" alt="image" src="https://github.com/user-attachments/assets/1af078f4-8e65-49bb-9ab0-3f181ed4ddd5" />

Un cop dins la màquina he instal·lat els paquets necessaris per instal·lar ldap al servidor.

<img width="729" height="387" alt="image" src="https://github.com/user-attachments/assets/fae01241-cf62-4679-bcaa-4320ea1f1792" />

A continuació ens demana la contrasenya de administració.

<img width="741" height="439" alt="image" src="https://github.com/user-attachments/assets/0bf862f7-5ea6-438a-a427-f6fa4e439fb6" />

Un cop instal·lat iniciare el proces de configuració automàtica de ldap.

<img width="536" height="35" alt="image" src="https://github.com/user-attachments/assets/11435f65-aab7-4cee-a09b-344108f22241" />

Ara li poso un nom al domini en el meu cas marc.com.

<img width="1190" height="348" alt="image" src="https://github.com/user-attachments/assets/624e5aaa-22b3-45c1-b05e-0180809460af" />

I un nom d'organització.

<img width="1004" height="271" alt="image" src="https://github.com/user-attachments/assets/256d9b19-d5ed-4570-9b4f-22f130b64595" />

I finalment la contrasenya d'administrador.

<img width="1054" height="251" alt="image" src="https://github.com/user-attachments/assets/399f8d56-1f0b-48ea-aa3a-22a90fad0695" />

Una veada configurat ja puc comprovar amb la comanda slapcat que existeix el servidor slap amb la configuració de nom de domini.

<img width="493" height="327" alt="image" src="https://github.com/user-attachments/assets/fff25ab4-f804-4025-97dc-59ebaa4a0b71" />

## Fitxers ldif

Ara he creat una nova unitat organitzativa anomenada users dins del domini marc.com.

<img width="724" height="163" alt="image" src="https://github.com/user-attachments/assets/6cd2f4f3-3e6f-4c95-bb68-e253ac9748c6" />

També he creat el fitxer grup.ldif on afegire un nou grup asocciat a una unitat organitzativa.

<img width="681" height="156" alt="image" src="https://github.com/user-attachments/assets/58bdda4f-9d9a-41fb-964c-9146c155309d" />

I finalment he creat un fitxer usuari.ldif on assigno un nou usuari anomenat alu1 on també li assinare un directori personal. 

<img width="680" height="385" alt="image" src="https://github.com/user-attachments/assets/f9412ef7-55f3-4ea8-9090-880411a8d9a8" />

## Comandes LDAP

A continuació es detalla l'ús i la gestió del directori LDAP mitjançant les comandes de terminal principals (`ldapadd`, `ldapsearch`, `ldapmodify` i `ldapdelete`), ordenades lògicament:

### 1. ldapadd

Un cop creats els fitxers LDIF, els hem d'afegir al servidor LDAP mitjançant la comanda `ldapadd`:

<img width="810" height="101" alt="image" src="https://github.com/user-attachments/assets/60b01fc9-5657-403f-bd31-1bf26619f663" />

<img width="809" height="78" alt="image" src="https://github.com/user-attachments/assets/e548b836-2014-44e5-beff-2b8df98b0985" />

<img width="809" height="78" alt="image" src="https://github.com/user-attachments/assets/3d0fc4fe-d270-46aa-9e61-9ae83b949640" />

I ara, mitjançant la comanda `slapcat`, podem comprovar els objectes que s'han creat correctament:

* **Unitat organitzativa:**
  <img width="514" height="209" alt="image" src="https://github.com/user-attachments/assets/5500de3e-84db-4c45-8c89-fa721398d8b2" />

* **Grup:**
  <img width="501" height="256" alt="image" src="https://github.com/user-attachments/assets/de0dd4e3-1442-4f9f-bd48-e3b7e5a11a10" />

* **Usuari:**
  <img width="506" height="495" alt="image" src="https://github.com/user-attachments/assets/14a7f2dc-237c-489b-8808-1bc5ef610a3e" />

### 2. ldapsearch

Amb la comanda `ldapsearch` podem fer cerques i consultes dels objectes de la base de dades del servidor LDAP:

* **Cerca de l'usuari `alu1` al domini `marc.com`:**
  En aquest exemple realitzem una cerca de l'usuari per verificar que es mostra correctament:
  <img width="794" height="652" alt="image" src="https://github.com/user-attachments/assets/bb8d68d4-7d5a-440a-9e29-7e6be710b436" />

* **Cerca general dels objectes creats al domini `marc.com`:**
  <img width="795" height="53" alt="image" src="https://github.com/user-attachments/assets/addfd714-1088-4b34-8d68-11f46be6d1cc" />

* **Cerca per a la comprovació de les Unitats Organitzatives (UOs) del domini:**
  <img width="984" height="106" alt="image" src="https://github.com/user-attachments/assets/3cc34d37-32ea-49a7-b632-3ef7ba1de9d7" />

### 3. ldapmodify

Per fer modificacions en els atributs dels objectes existents al directori (com ara canviar contrasenyes), s'utilitza la comanda `ldapmodify` acompanyada d'un fitxer LDIF de modificació.

A continuació, modifiquem la contrasenya de l'usuari `alu1`. Primer creem el fitxer `modify.ldif`:
<img width="571" height="29" alt="image" src="https://github.com/user-attachments/assets/20f5bdc4-2a3b-41c0-8d24-47e717a3294c" />

El contingut d'aquest fitxer per canviar la contrasenya a `marc1234` és el següent:
<img width="718" height="106" alt="image" src="https://github.com/user-attachments/assets/d580c5ce-7bc5-46c0-a194-5c2763762a03" />

I finalment, apliquem aquest fitxer de modificació al servidor LDAP:
<img width="914" height="85" alt="image" src="https://github.com/user-attachments/assets/4633f38a-d8fc-439a-b8a4-695c05cfc52e" />

### 4. ldapdelete

La comanda `ldapdelete` ens permet eliminar objectes directament del directori LDAP sense necessitat de crear cap fitxer LDIF addicional, indicant directament el DN (Distinguished Name) de l'entrada que volem esborrar:

<img width="1088" height="100" alt="image" src="https://github.com/user-attachments/assets/655a69a2-56d5-4771-9756-6ba20ed20980" />

## Unio client al domini

Com he dit abans he configurat la màquina servidor amb Xarxa NAT, per tant el client també el configurare dins de la mateixa Xarxa NAT.

<img width="662" height="225" alt="image" src="https://github.com/user-attachments/assets/374cd032-e41c-4945-819f-928445d9bf5b" />

<img width="741" height="278" alt="image" src="https://github.com/user-attachments/assets/266aa293-0cd1-435f-939c-22944d31deed" />

Primer comprobo de fer un ping desde el client al servidor.

<img width="623" height="227" alt="image" src="https://github.com/user-attachments/assets/6e80d8a2-a118-40c0-b601-ad2b0464ded3" />

Un cop comprobada la xarxa instal·lare el paquet necessari per connectarme del client al servidor.

<img width="768" height="73" alt="image" src="https://github.com/user-attachments/assets/27017b8a-f3c7-4edb-a00b-02768c1ff96a" />

I ens sortira aquest menú de configuració.
Primer posem la IP del sercidor 10.0.2.15.

<img width="1187" height="276" alt="image" src="https://github.com/user-attachments/assets/6115b3b6-2ffe-456b-b8f9-3c01bed12ce0" />

Poso el nom del domini al qual em vull connectar que és marc.com

<img width="1167" height="234" alt="image" src="https://github.com/user-attachments/assets/5e821562-37e7-42de-8809-c61102a5672c" />

<img width="1151" height="279" alt="image" src="https://github.com/user-attachments/assets/4cd00275-43b1-4500-8ea8-a8900d0d45bc" />

Ens pregunta de sí el ldap necessita de autenticació amb contrasenya direm que sí.

<img width="837" height="249" alt="image" src="https://github.com/user-attachments/assets/78c9207a-8bd7-4bbb-90d1-e89070f05f17" />

I el compte root de ldap.

<img width="577" height="252" alt="image" src="https://github.com/user-attachments/assets/8e82da28-c94c-43a3-b23e-619d1505bc31" />

Finalment ens demana la contrasenya del servidor.

<img width="1188" height="293" alt="image" src="https://github.com/user-attachments/assets/416eaa63-a49b-4498-9de0-f105a66f10cf" />

I ara l'usuari sense privilegis.

<img width="1029" height="261" alt="image" src="https://github.com/user-attachments/assets/ffe81372-fb8f-4faf-b737-44e47565c852" />

I la contrasenya per accedir a la base de dades ldap.

<img width="757" height="225" alt="image" src="https://github.com/user-attachments/assets/2fac7786-d18b-41eb-83f3-93274a720c7e" />

I el hash per defecte que el deixarem en el vaor per defecte que és md5.

<img width="1156" height="586" alt="image" src="https://github.com/user-attachments/assets/0ee14d01-f6d8-49cf-b2e4-cd382a8d6855" />

També és molt important editar el fitxer nsswitch per garantitzar la autenticació i no la busqueda de fitxer locals per accedir al servidor.

<img width="783" height="210" alt="image" src="https://github.com/user-attachments/assets/18359099-0678-4ac4-9829-8d2d638a7622" />

Finalment afegeixo aquesta línia al arxiu common-session per crear el directori home dels usuaris amb umask 022.

<img width="876" height="634" alt="image" src="https://github.com/user-attachments/assets/9cdd69f5-9d6f-491f-a366-542ff51262e8" />

I desde el servidor ja puc comprovar que troba l'usuari alu1.
<img width="546" height="44" alt="image" src="https://github.com/user-attachments/assets/81b660d9-bf87-44c4-afb2-4930ba9ec733" />

I ara probare d'accedir gràficament.

<img width="288" height="68" alt="image" src="https://github.com/user-attachments/assets/c77c6b78-1721-498e-90ed-983223e73268" />

## CONFIGURACIÓ LDAP ENTORN GRÀFIC

En primer lloc instal·lare al servidor l'eina d'etorn gràfic per configurar ldap.

<img width="1053" height="524" alt="image" src="https://github.com/user-attachments/assets/6ee5d35b-d60d-4e2c-b59c-2467b35f4735" />

<img width="327" height="214" alt="image" src="https://github.com/user-attachments/assets/3fad02a2-2acd-43ae-8750-d0f7e074b5c1" />

És necessari instal·lar java per iniciar apache.

<img width="865" height="328" alt="image" src="https://github.com/user-attachments/assets/b5c8a432-c935-4f9d-ab23-e24fd22504a6" />

<img width="620" height="333" alt="image" src="https://github.com/user-attachments/assets/bc0eb7cb-26e9-42d2-827c-f365b1eefcc2" />

Ara estableixo la connexió al servidor amb la IP del servidor.

<img width="622" height="712" alt="image" src="https://github.com/user-attachments/assets/016e41c8-b398-41af-9eec-e30a6b6a4466" />

Poso les dades de autenticació del servidor.

<img width="615" height="715" alt="image" src="https://github.com/user-attachments/assets/c5c9e07f-1d9e-4390-879b-f7f58f0a346f" />

I ja estic connectat al servidor LDAP.

<img width="907" height="316" alt="image" src="https://github.com/user-attachments/assets/21b7c03b-9fde-4c0f-b889-8b2d6072890a" />

I podem crear nous templates de forma gràfica.

<img width="621" height="588" alt="image" src="https://github.com/user-attachments/assets/328ea5bb-935b-4460-9ddb-33fc66c384df" />

Per exemple una nova UO.
<img width="622" height="269" alt="image" src="https://github.com/user-attachments/assets/31c3893e-7bcf-408e-ae3a-983f8ee510ad" />

<img width="610" height="293" alt="image" src="https://github.com/user-attachments/assets/aeb23171-83ec-4e73-b4f2-9b4f24497bef" />

Aquesta forma és molt més sencilla i entenedora per un usuari no expert per tant facilita la manipulació del servidor ldap.
<img width="206" height="55" alt="image" src="https://github.com/user-attachments/assets/f8484630-c873-4588-8b37-483cc2958df9" />

## SERVIDORS NFS

El protocol NFS (Network File System) ens permet compartir directoris i fitxers a través de la xarxa local, de manera que els clients els puguin muntar en el seu sistema com si fossin carpetes locals. L'autenticació en NFS es realitza principalment a nivell de màquina (host), confiant en els equips de la xarxa als quals donem accés. En aquest apartat, veurem la configuració del servidor, de clients Ubuntu i Windows, i finalment com integrar-ho amb LDAP per muntar de forma automàtica els directoris personals (home) dels usuaris del domini.

### 1. Instal·lació del Servidor NFS

Per començar, instal·larem el programari del servidor NFS a la màquina servidor d'Ubuntu. Per fer-ho, actualitzem els repositoris i instal·lem el paquet corresponent:

```bash
sudo apt update
sudo apt install nfs-kernel-server
```

![Instal·lació de nfs-kernel-server](NFS1.png)

Un cop completada la instal·lació, verifiquem l'estat del servei per assegurar-nos que s'està executant correctament:

```bash
sudo systemctl status nfs-server
```

![Estat del servei nfs-server](NFS2.png)

---

### 2. Instal·lació del Client NFS en Ubuntu

A la màquina client amb sistema operatiu Ubuntu, necessitem instal·lar el paquet client per poder muntar els recursos NFS que exporti el servidor:

```bash
sudo apt update
sudo apt install nfs-common rpcbind
```

![Instal·lació del client NFS en Ubuntu](NFS3.png)

---

### 3. Instal·lació del Client NFS en Windows

Per tal de connectar un client amb sistema operatiu Windows al servidor NFS, hem d'activar la característica corresponent del sistema:

1. Ens dirigim al **Panell de control** > **Programes** > **Programes i característiques**.
2. Al menú de l'esquerra, seleccionem **Activa o desactiva característiques de Windows**.
3. Busquem la branca **Serveis per a NFS** i activem la casella **Client per a NFS**.

![Activació del servei NFS a Windows 1](NFS4.png)
![Activació del servei NFS a Windows 2](NFS5.png)

---

### 4. Ús del Servidor NFS i Compartició de Fitxers

#### A. Configuració al Servidor

En primer lloc, creem la carpeta que volem compartir (per exemple, `/compartida`), li assignem propietari i grup com a `nobody` i `nogroup` per a l'accés genèric, i li configurem els permisos adequats perquè tothom pugui llegir i escriure:

```bash
sudo mkdir /compartida
sudo chown nobody:nogroup /compartida
sudo chmod 777 /compartida
ls -ld /compartida
```

![Creació i permisos de la carpeta compartida](NFS6.png)

Per exportar aquesta carpeta a la xarxa, editem el fitxer de configuració de comparticions de NFS `/etc/exports`:

```bash
sudo nano /etc/exports
```

Dins d'aquest fitxer, afegim la línia per compartir `/compartida` amb tots els clients (`*`) amb permisos de lectura i escriptura (`rw`), sincronització immediata (`sync`) i desactivant la comprovació de subarbres per millorar el rendiment (`no_subtree_check`):

```text
/compartida *(rw,sync,no_subtree_check)
```

![Edició de /etc/exports per a la carpeta compartida](NFS7.png)

Després de modificar `/etc/exports`, reiniciem el servei NFS per aplicar els canvis. També podem crear un fitxer de prova buit dins del directori compartit per comprovar posteriorment la lectura des dels clients:

```bash
sudo systemctl restart nfs-kernel-server
sudo touch /compartida/hola
```

![Reinici del servei i creació d'arxiu de prova](NFS8.png)

#### B. Proves de connexió des de Windows

Ara passem al client Windows per connectar-nos al recurs. Obrim l'explorador de fitxers i ens dirigim a la IP del servidor (per exemple, `\\10.0.2.16`) per veure els recursos disponibles:

![Accés al servidor des de Windows](NFS9.png)

Podrem observar que apareix la carpeta `compartida`. Si hi entrem, veurem el fitxer `hola` que hem creat des del servidor:

![Contingut de la carpeta compartida a Windows](NFS10.png)

Per provar els permisos d'escriptura des de Windows, creem un nou arxiu de text anomenat `mrworldwide.txt` a dins:

![Creació d'arxiu des de Windows](NFS11.png)

Si tornem al servidor i llistem els detalls de la carpeta, veurem que el nou arxiu té uns ID de propietari i grup específics associats a l'usuari anònim de Windows:

![Verificació d'arxiu de Windows al servidor](NFS12.png)

#### C. Proves de connexió des del Client Ubuntu

Ara farem la mateixa prova en el nostre client Ubuntu. Creem un directori local per al punt de muntatge (per exemple, `/mnt/nfs`), li donem permisos totals i procedim a muntar el recurs compartit indicant la IP del servidor:

```bash
sudo mkdir -p /mnt/nfs
sudo chmod 777 /mnt/nfs
sudo mount 10.0.2.16:/compartida /mnt/nfs/
df -h
```

![Muntatge de la carpeta compartida a Ubuntu](NFS13.png)

Si llistem el contingut del punt de muntatge local, veurem tant el fitxer `hola` original com l'arxiu creat per Windows:

```bash
ls -l /mnt/nfs
```

![Visualització de fitxers des del client Ubuntu](NFS14.png)

Finalment, creem un arxiu des del client Ubuntu per assegurar-nos que tenim drets d'escriptura. En llistar-lo, observem que el propietari es maps automàticament a `nobody:nogroup`:

```bash
touch /mnt/nfs/asdf
ls -l /mnt/nfs
```

![Creació de fitxer des d'Ubuntu](NFS15.png)

---

### 5. Integració de NFS amb usuaris LDAP

Una de les utilitats principals d'integrar NFS amb LDAP es permetre que els directoris personals (`/home/nom_usuari`) estiguin centralitzats al servidor i es muntin dinàmicament a la màquina client quan l'usuari inicia la sessió.

#### A. Configuració al Servidor NFS

Primer, preparem un nou directori al servidor NFS destinat a allotjar els perfils dels usuaris (per exemple, `/perfils`). Editem de nou el fitxer `/etc/exports`:

```text
/perfils *(rw,sync,no_subtree_check)
```

![Configuració de /perfils a /etc/exports](NFS16.png)

Creem la carpeta al disc del servidor, li assignem com a propietari `nobody:nogroup` i donem permisos totals de lectura/escriptura, reiniciant el servidor NFS a continuació:

```bash
sudo mkdir /perfils
sudo chown nobody:nogroup /perfils
sudo chmod 777 /perfils
sudo systemctl restart nfs-kernel-server
```

![Creació del directori /perfils i reinici del servei](NFS17.png)

#### B. Modificació del Servidor LDAP per a l'usuari

Perquè el client sàpiga que el directori de l'usuari està localitzat a `/perfils/alu4`, hem de crear o modificar l'usuari en el directori LDAP. Creem un fitxer LDIF (per exemple, `usu.ldif`) definint el nou usuari `alu4` i assignant-li la propietat `homeDirectory` apuntant a la ruta centralitzada:

```text
dn: uid=alu4,ou=users,dc=sabate,dc=cat
objectClass: inetOrgPerson
objectClass: posixAccount
objectClass: shadowAccount
cn: alu4
sn: alu4
uid: alu4
uidNumber: 2004
gidNumber: 2001
homeDirectory: /perfils/alu4
loginShell: /bin/bash
```

![Creació del fitxer usu.ldif per a LDAP](LDAPF.png)

Afegim aquest usuari a la base de dades del servidor LDAP:

```bash
ldapadd -x -D "cn=admin,dc=sabate,dc=cat" -w marc -f usu.ldif
```

![Addició de l'usuari alu4 al LDAP](LDAPF2.png)

#### C. Configuració del Client per al muntatge automàtic

Al client Ubuntu, per tal que en arrencar el sistema es munti el directori centralitzat `/perfils`, primer creem la carpeta corresponent i li assignem permisos amplis:

```bash
sudo mkdir /perfils
sudo chmod 777 /perfils
```

![Creació del directori /perfils al client](LDAPF3.png)

A continuació, editem el fitxer de configuració de muntatges estàtics `/etc/fstab` perquè munti automàticament la carpeta `/perfils` en iniciar-se el client:

```text
10.0.2.16:/perfils /perfils nfs auto,noatime,nolock,bg,nfsvers=3,intr,tcp,actimeo=1800 0 0
```

![Configuració de fstab al client](LDAPF4.png)

#### D. Inici de sessió de l'usuari LDAP al Client

Finalment, reiniciem el client. A la pantalla de login escollim l'opció per introduir l'usuari manualment i iniciem la sessió amb les credencials de l'usuari `alu4`. El sistema reconeixerà l'usuari a través de LDAP, muntarà el seu directori d'usuari a través de NFS a `/perfils/alu4` i el crearà automàticament.

![Inici de sessió correcte al client amb alu4](LDAPF5.png)

Si obrim un terminal dins d'aquesta sessió, comprovem amb `whoami` que hem entrat com a `alu4`, i el sistema ens situarà automàticament a la seva home centralitzada:

```bash
whoami
pwd
```

![Comprovació de l'usuari alu4 al client](LDAPF6.png)

## SAMBA

Per començar amb la configuració de Samba, instal·lo el paquet necessari al servidor.

```markdown
![alt text](image-1.png)

Aquí es pot veure el procés d'instal·lació del paquet samba al servidor.
```
Un cop instal·lat, comprovo l'estat del servei per assegurar-me que s'està executant correctament.

![alt text](image-2.png)

A continuació, creo la carpeta que vull compartir i li assigno els permisos necessaris perquè els usuaris hi puguin accedir.

![alt text](image-3.png)
![alt text](image-4.png)

Ara edito el fitxer de configuració principal de Samba `/etc/samba/smb.conf`.

![alt text](image-5.png)

Dins del fitxer, defineixo el recurs compartit amb la seva ruta i els permisos de lectura/escriptura.

![alt text](image-6.png)

Utilitzo la comanda `testparm` per verificar que no hi hagi errors de sintaxi en la configuració.

![alt text](image-7.png)

Reinicio els serveis de Samba per aplicar els canvis realitzats.

![alt text](image-8.png)

Creo un usuari al sistema que serà el que utilitzarem per connectar-nos des del client.

![alt text](image-9.png)

I li assigno una contrasenya específica per al servei Samba mitjançant `smbpasswd`.

![alt text](image-10.png)

Configuro el tallafocs (ufw) per permetre el trànsit de dades de Samba.

![alt text](image-11.png)

Des del client, comprovo primer la connectivitat amb el servidor.

![alt text](image-12.png)

Instal·lo el paquet `cifs-utils` al client per poder muntar unitats de xarxa.

![alt text](image-13.png)

Intento accedir al recurs compartit mitjançant l'explorador de fitxers utilitzant la IP del servidor.

![alt text](image-14.png)

El sistema ens demanarà les credencials de l'usuari que hem creat prèviament.

![alt text](image-15.png)

Un cop autenticats, ja podem veure el contingut de la carpeta compartida.

![alt text](image-16.png)

Faig una prova creant un fitxer des del client per comprovar que tenim permisos d'escriptura.

![alt text](image-17.png)

Comprovo al servidor que el fitxer s'ha creat correctament.

![alt text](image-18.png)

Per automatitzar el procés, configuro el fitxer `/etc/fstab` al client per muntar la carpeta en iniciar el sistema.

![alt text](image-19.png)

Executo el muntatge manualment per verificar que la línia del fstab és correcta.

![alt text](image-20.png)

Finalment, verifico que el punt de muntatge està actiu i accessible.

![alt text](image-21.png)
