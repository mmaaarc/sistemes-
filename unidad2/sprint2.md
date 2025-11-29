---
layout: default
title: Sprint 2 - Título del Contenido
---
Sprint2

 



Introducció
-----------

En aquest sprint veurem com es gestionen els usuaris, grups i permisos d'un sistema en Linux. També configurarem les polítiques de seguretat per a comptes d'usuaris i per al sistema. Instal·larem i configurarem serveis i processos essencials del sistema operatiu, crearem i administrarem sistesmes de fitxers i noces particions. Implementarem un sistema de còpies de seguretat i per últim farem proves per comprovar el funcionament del sistema.

Gestió de processos
===================

*   En primer lloc definirem un procés. Aquest es un programa en execució que inclou dins seu: el seu codi, els recursos que te assignats i la seva execució. El procesos de linux poden ser en primer o en segon pla. Els que estàn en primer pla implequen una interacció amb l'usuari mentre que als de segon pla no es requereix aquesta interacció.
*   La primera comada que utilitzarem per llistar els procesos es "pstree", aquesta ens mostrarà els processos actius que hi ha i quins son els seus fills si es que en té, tot això amb forma d'arbre, d'aquí el nom.
    
    `[](#__codelineno-0-1)pstree`
    
    ![procesos1](../img/ps.png) 
    ![procesos2](../procesos2.png)
*   Amb la mateixa comanda si volem saber a l'usuari que correspon i a quin número de procés tenim ho podem realitzar amb les lletres h (usuari) i p (procés).
    
    <img width="997" height="587" alt="pss" src="https://github.com/user-attachments/assets/55c3f6c6-42f1-472d-9864-7fee2b288cf4" />

*   A continuació veurem com matar un procés, per això serà necessari saber quin número de procés li correspon a cadascun d'aquestos. En el cas de matar un procés pare tots els processos fills haurien de morir, tot i que hi ha una possibiltat de que algún quedi viu, i aquestos s'anomenen zombies.
*   Per matar un procés utilitzarem la seguent comanda i el número de procés:
    
<img width="401" height="53" alt="image" src="https://github.com/user-attachments/assets/7b6ac67b-5168-4905-83ec-8be42af7e21a" />
    
*   Per fer la prova he utilitzat un altre terminal i m'he guardat el seu PID, per matar el procés tal i com es demostra a continuació:
<img width="995" height="306" alt="prov" src="https://github.com/user-attachments/assets/5413851c-77ae-4224-8a0f-1adb08394575" />

<img width="997" height="105" alt="killl" src="https://github.com/user-attachments/assets/a48e391c-2055-4024-af45-65ac9b3cfbe8" />

<img width="1000" height="132" alt="gnome" src="https://github.com/user-attachments/assets/67f757e9-11fb-4f03-88d3-529899d23103" />

*   La comanda anterior fa una imatge dels processos, aquestos no canvien en temps real, per fer una consulta d'aquest tipus utilitzarem la comanda "top".

<img width="809" height="527" alt="image" src="https://github.com/user-attachments/assets/711cb650-fa9b-4ea6-a8ff-3deebbdb4ca4" />

    
*   Aquesta comanda ens dona molta informació per columnes, i ara veurem que vol dir cada columna. PID: Identificador únic del procés. USER: Usuari que inicia el procés. %CPU: Percentatge d'ús del processador. %MEM: Percentatge d'ús de la memòria RAM. COMMAND: Nom de la comanda o programa.
<img width="1000" height="241" alt="term" src="https://github.com/user-attachments/assets/7672e4fb-8d6b-4829-9dff-99ce37fa1c0b" />

*   En cas d'obrir un nou procés (ex: navegador) aquest ens apareixerà.
  <img width="1003" height="64" alt="vv" src="https://github.com/user-attachments/assets/65274143-a389-4eb5-ba04-5cf391a505d0" />

*   La prioritat no es pot modificar directament, però amb el NI (nice) si que es pot canviar, contra mes baix es el número més prioritat té. Això es pot fer amb la següent comanda. Val a dir que caldria fer-ho des de el root ja que com sabem ens otorga més privilegis.

`[](#__codelineno-4-1)renice -n -nºprioritat -p PID`

<img width="1021" height="64" alt="da" src="https://github.com/user-attachments/assets/ccda0c72-03a6-4d4f-92ec-ca06d16cf5e2" />

<img width="1033" height="28" alt="fd" src="https://github.com/user-attachments/assets/258b10bc-ef08-45f9-a89b-999f0a9390cc" />

- Aquesta comanda serveix per moments determinats la prioritat per renice no es permanent. - Seguidament també podem utilitzar la comanda "ps aux" que ens dona una informació similar però amb diferents parametres que veurem a continuació: USER: Usuari que ha iniciat el procés. PID: Identificador únic del procés. %CPU i %MEM: Percentatge de CPU i memòria RAM utilitzats pel procés. VSZ: Memòria virtual total utilitzada pel procés. RSS: Memòria física utilitzada pel procés. TTY: Terminal associat al procés ( ? si no en te). STAT: Estat del procés. R Executant-se (Running). S = Inactiu. T = Pausat. Z = Procés zombi. I = Inactiu o sense consumir recursos. < = Alta prioritat de CPU. s = Líder de sessió. l = Multithread. + = Associat al terminal en primer pla.

`[](#__codelineno-5-1)ps aux`

<img width="1036" height="616" alt="aux" src="https://github.com/user-attachments/assets/d9192ceb-47c4-456c-8a71-dedf9b30afb8" />


- Amb el ps podem fer varies combinacions per mostrar informació en concret a continuació veurem quines són i que fan.

`[](#__codelineno-6-1)ps -e`

\- Mostra tots els procesos del sistema amb una sintaxis estandar.

`[](#__codelineno-7-1)ps -ejH`

\- Mostra un arbre de procesos-

`[](#__codelineno-8-1)ps -eLf`

\- Mostra la informació dels fils (threads).

`[](#__codelineno-9-1)ps -eM`

\- Mostra informació de seguretat

`[](#__codelineno-10-1)ps -U`

\- Mostra tots els processos de root.

*   A continuació veurem que són els processos amb segon pla i com passar processos a aquest estat. Com hem dit abans amb el kill -9 matem un procés i amb el ctrl+c l'aturem i amb el ctrl+z si que el passariem a segon pla. (Nota: segons el tipus de procés que aturem, si aquest va per terminal igaul no se'ns mostra en segon pla).
*   La comada per veure els processos en segon pla es la següent.
    
    `[](#__codelineno-11-1)jobs`

   <img width="996" height="85" alt="jobs" src="https://github.com/user-attachments/assets/f8cdc2e2-ac60-4a5a-8ff8-5d847f3548a7" />

*   Un cop tenim aquest procés localitzat i no volem matar-lo sino que el volem enviar al primer pla podem utilitzar la següent comanda.

<img width="1001" height="36" alt="z" src="https://github.com/user-attachments/assets/f2388788-aa72-428c-aaa9-35fdd035eacf" />

<img width="1207" height="713" alt="procesos14" src="https://github.com/user-attachments/assets/f88e3e71-4499-423f-a64d-7796ed0cbfee" />

<img width="1207" height="129" alt="procesos15" src="https://github.com/user-attachments/assets/73352b91-7548-4322-8691-4d389e29810e" />

*   En cas de voler fer el procés invers i enviar un procés al segon pla podem utilitzar:
    
    `[](#__codelineno-13-1)bg %nº`
    
*   En algun cas espacial igual volderm executar algun procés directament amb segon pla, i es pot fer de la seguent forma.
    
    `[](#__codelineno-14-1)nomproces &`
    
*   A l'hora de consultar processos amb top em vist que es una eina en viu i que els processos que volem consultar es van movent i, a vegades se'ns pot fer complicat llegir-lo. En cas de voler evitar això i sol consultar el PID d'un procés en concret podem fer servir la següent comanda.
  
<img width="1207" height="81" alt="procesos16" src="https://github.com/user-attachments/assets/09c1efd8-b3ac-4c23-8230-b9c21597a698" />

        
*   Un altra forma de fer-ho podria ser utilitzant comandes anteriors i afegir un grep, pero en algunes opcions com el ps aux pot quedar una mica confós, personalment ho recomano amb el pstree ja que així veurem també els processos fills.
   <img width="1207" height="81" alt="procesos17" src="https://github.com/user-attachments/assets/110e7f30-bb99-4468-a3b9-28c2fef3cb92" />
 
    
*   Per acabar, si en algun moment volem utilitzar algún script o procés i que aquest tingui una prioritat predeterminada per nosaltres es pot fer amb el nice.
    
    <img width="1207" height="127" alt="procesos18" src="https://github.com/user-attachments/assets/e37c94ae-383d-4593-b052-e703a48f83d3" />

*   Amb un "top" podem comprovar si ha funcionat correctament. ![procesos19](../img/procesos19.png)

Gestió d'usuaris grups i permisos
=================================

*   Es important que al nostres sistema tinguem diferents usuaris i que aquestos tinguen diferents caracteristiques, i que els puguem incloure en grups per classificar-los. A més a més, també ens interessarà poder modificar-los, eliminar-los i bloquejar-los al nostre gust. Tot això i més ho veurem a continuació.

\- Commandes terminal i accessos als directoris
-----------------------------------------------

Per a accedir al terminal normalment ho faremt amb un crtl + alt + t, així obrim el pseudo terminal. El terminal com a tal l'obrirem al el ctrl dret + F3, aquest es un terminal TTY. Un pseudo terminal es com un emulador on les comandes que posem son interpretades per algún arxiu al que fan referencia i aquest fa els procediments, en canvi amb un terminal si que estem amb contacte directe amb el sistema.

*   En primer lloc veurem un document que actua com un registre de tots els comptes d'usuaris presents al sistema. Inclou dades com el nom del compte, l'identificador d'usuari (UID), el directori personal i el shell configurat per defecte. Es tracta d'un fitxer públic, cosa que permet que qualsevol pugui consultar qui són els usuaris del sistema.
    
    `[](#__codelineno-18-1)nano /etc/passwd`
    
    ![gestiousu1](../img/gestiousu1.png)
*   A continuació podem veure els grups dels usuaris i l'identificador de qui es el seu administrador.
    
    `[](#__codelineno-19-1)nano /etc/group`
    
    ![gestiousu2](../img/gestiousu2.png)
*   A continuació, en aquest arxiu es guarda la informació relacionada amb les contrasenyes dels comptes d'usuari. Cada registre fa referència a un usuari i inclou la seva contrasenya codificada. Si apareix el símbol "!", això indica que el compte està deshabilitat i l'usuari no té permís per accedir al sistema.
    
    `[](#__codelineno-20-1)nano /etc/shadow`
    
    ![gestiousu3](../img/gestiousu3.png)
*   Per últim aquest arxiu és comparable a /etc/group, però ofereix detalls extres sobre els grups. En aquest lloc es pot identificar qui són els administradors de cada grup. Resulta pràctic per controlar els permisos i gestionar els privilegis d'accés dels diferents grups d'usuaris.
    
    `[](#__codelineno-21-1)nano /etc/gshadow`
    
    ![gestiousu4](../img/gestiousu4.png)

\- Creació d'usuaris
--------------------

Per crear usuaris tenim diverses formes de fer-ho, el més important es tenir clar que amb certes comandes no es creen directoris sol usuaris. A continuació es mostrarà com crear usuaris.

*   En primer lloc utilitzarem la següent comanda, aquesta ens creara un usuari pero fins que no fessim un log in amb aquest no ens crearà els directoris. Aquesta es la forma més senzilla de crear els usuaris ja que et ve pautada pel propi sistema operatiu.
    
    `[](#__codelineno-22-1)adduser usuari`
    
    ![gestiousu5](../img/gestiousu5.png) Per crear un nou compte d'usuari al sistema, farem servir la comanda useradd. Aquesta comanda ens permetrà afegir usuaris al sistema amb diversos paràmetres que ens ajuden a configurar les seves propietats. A continuació, detallem alguns dels paràmetres més destacats que podem utilitzar:
    
*   \-m: Indica que es generarà automàticament un directori personal per a l'usuari.
    
*   \-s /bin/bash: Aquest paràmetre ens permet definir el shell per defecte de l'usuari.
    
*   \-d /home/alumne2: Amb aquest paràmetre, especifiquem el directori inicial de l'usuari. Per exemple, en aquest cas, el directori personal serà /home/alumne2.
    
*   alumne2: Correspon al nom de l'usuari que estem creant. En aquest exemple, l'usuari es dirà "alumne2".
    
*   && passwd alumne2: Aquesta comanda s’utilitza per assignar o modificar la contrasenya de l’usuari "alumne".
    

`[](#__codelineno-23-1)useradd usuari`

![gestiousu6](../img/gestiousu6.png) - Sino utilitzem la comanda -m per als directoris els podem afegir de la següetn manera.

`[](#__codelineno-24-1)mkdir usuari`

![gestiousu7](../img/gestiousu7.png) ![gestiousu8](../img/gestiousu8.png)

*   Si volem canviar el nom de l'usuari podem utilitzar la següent comanda. EN el cas que hi ha a continuació volem canviar el nom d'usuari de porva2, ja que hauria de ser prova2.

`[](#__codelineno-25-1)usermod -l usernou user`

![gestiousu15](../img/gestiousu15.png) ![gestiousu16](../img/gestiousu16.png) ![gestiousu17](../img/gestiousu17.png)

*   En cas de voler eliminar accés a un usari ho podem fer bloquejant-lo, la comanda seria la següent. Una forma de comprovar que s'ha bloquejat correctament es entrar a la carpeta de passwd i veurem que la contrasenya del usuari al davant té un signe d'exclamació "!"

`[](#__codelineno-26-1)usermod -L usuari`

![gestiousu9](../img/gestiousu9.png) ![gestiousu10](../img/gestiousu10.png) - Seguint amb la creació d'usuaris, si tenim un usuari bloquejat i el volem recuperar utilitzarem aquesta comanda. A l'hora de comprovar-ho ens fixarem que ja no te l'exclamació.

`[](#__codelineno-27-1)usermod -U usuari`

![gestiousu13](../img/gestiousu13.png) - Si realment el que volem es eliminar l'usuari de forma més permanent ho farem amb la següent comanda. Per comprovar si l'hem eliminat correctament podem entrar a la carpeta passwd i veurem que l'usuari ja no hi es.

`[](#__codelineno-28-1)deluser usuari`

![gestiousu11](../img/gestiousu11.png) ![gestiousu12](../img/gestiousu12.png)

*   Per complementar una mica les comandes que tenim, aquí en tenim algunes que ens poden ajudar també, la següent elimina la "home" de l'usuari.
    
    `[](#__codelineno-29-1)rm -r usuari`
    
*   Un dels problemes habituals es que no eliminem les homes i directoris dels usuaris, amb la següent comanda ho podem fer tot a la vegada.
    
    `[](#__codelineno-30-1)userdel -r usuari`
    
*   En cas de voler consultar algun tipus d'informació sobre algun usuari, podem fer-ho així.
    
    `[](#__codelineno-31-1)id usuari`
    
    ![gestiousu18](../img/gestiousu18.png)
*   Un cop vist com es el funcionament a través del terminal podrem observar com es fa per l'interficie gràfica d'Ubuntu. Dins de la configuració de sistema hem d'entrar a l'apartat usuaris, i després seguirem els passos que hi ha a continuació. ![gestiousunou1](../gestiousunou1.png) ![gestiousunou2](../img/gestiousunou2.png) ![gestiousunou3](../img/gestiousunou3.png) ![gestiousunou4](../img/gestiousunou4.png) ![gestiousunou5](../img/gestiousunou5.png)

\- Creació de grups
-------------------

*   En aquest apartat veurem com funcionen els grups d'usuaris, com hem vist anteriorment podem consultar els grups i les seves contrasenyes. Important dir que quan es crea un usuari també es crea un grup amb el nom d'aquest.
*   Per crear un grup nou ho podem fer amb una senzilla comanda.
    
    `[](#__codelineno-32-1)addgroup grup`
    
    ![gestiogrup](../img/gestiogrup.png) ![gestiogrup1](../img/gestiogrup1.png)
    
*   D'altra banda si el que volem es afegir un usuari a un grup existent ho podem fer d'aquesta manera.
    
    `[](#__codelineno-33-1)adduser usuari grup`
    
    ![gestiogrup2](../img/gestiogrup2.png) ![gestiogrup3](../img/gestiogrup3.png)
    
*   L'operació anterior també es pot fer amb aquesta comanda.
    
    `[](#__codelineno-34-1)gpasswd -a usuari grup`
    
*   Per fer a un usuari administrador d'aquell grup ho podem fer així. Dins de la carpeta gshadow podem veure els usuaris i administradors dels grups, per reconeixels veurem la posició que tenen entre els ":", l'alumne 2 es administrador d'asix1 i membre d'asix2.
    
    `[](#__codelineno-35-1)gpasswd -A usuari grup`
    
    ![gestiogrup4](../img/gestiogrup4.png) ![gestiogrup5](../img/gestiogrup5.png)
    
*   Un dels majors problemes es que quan afegim usuaris a grups amb les comandes anteriors els treu del grup on estaven, per evitar-ho hem d'utilitzar la següent comanda. Com comprovarem l'usuari alumne2 forma part dels dos grups d'asix i es administrador del primer.
    
    `[](#__codelineno-36-1)usermod -a -G grup usuari` 
    
    ![gestiogrup6](../img/gestiogrup6.png) ![gestiogrup7](../img/gestiogrup7.png)
    
*   Per eliminar un usuari d'un grup ho farem com veurem a continuació. En aquest cas l'alumne2 ja te prous responsabilitats i l'eliminarem del grup d'asix1.
    
    `[](#__codelineno-37-1)gpasswd -d usuari grup`
    
    ![gestiogrups8](../img/gestiogrups8.png) ![gestiogrup9](../img/gestiogrup9.png)
    
*   L'anterior comanda també es pot fer amb aquesta altra
    
    `[](#__codelineno-38-1)deluser usuari grup`
    
    ![gestiogrup10](../img/gestiogrup10.png)
    
*   Per fer un usuari el principal d'un grup en concret utilitzarem el següent.
    
    `[](#__codelineno-39-1)usermod -g grup usuari`
    
*   En cas de voler canviar el nom d'algun grup ho farem amb la següent comanda.
    
    `[](#__codelineno-40-1)groupmod -n grupnou grupvell`
    
    ![gestiogrup11](../img/gestiogrup11.png) ![gestiogrup12](../img/gestiogrup12.png)

\- Configuració de fitxers d'usuari
-----------------------------------

*   Com hem vist tenim una serie de comandes per defecte que tenen una serie d'efectes sobre els usuaris que hem creat. Tot això es pot canviar, la seva útilitat resideix en que si volem que els nostres usuaris nous tinguin diferents directoris o inclús politiques de contrasenyes diferents. Ara veurem com es modifiquen els següents arxius.
*   El primer arixu que modificarem es el `/etc/default/useradd` que ens permet establir els valors predefinits per als nous usuaris, com la ruta del directori personal i el shell per defecte. Per configurar-lo utilitzem la següent comanda.
    
    `[](#__codelineno-41-1)nano /etc/default/useradd`
    
    Els parametres que es poden modificar son els següents:
*   GROUP: Especifica el grup que s'assignarà com a grup principal per defecte als nous usuaris. Si està comentat o no existeix, el sistema crea un grup nou per a cada nou usuari amb el mateix nom que l'usuari.
*   HOME: Defineix la ruta base per als directoris de casa dels nous usuaris. Per defecte, és /home. Si vols canviar la ubicació dels directoris de casa, pots modificar aquest paràmetre.
*   INACTIVE: Estableix el nombre de dies després dels quals una contrasenya expirada passarà a estar inactiu si no es canvia. Un valor de -1 desactiva aquesta funcionalitat.
*   EXPIRE: Data en què l'usuari expira, en format AAAAMMDD. Si està comentat o no s'especifica, l'usuari no expira mai.
*   SHELL: Indica el shell per defecte per als nous usuaris. El valor predeterminat és /bin/sh, però es pot canviar a /bin/bash o qualsevol altre shell disponible.
*   SKEL: Especifica el directori des del qual es copiaran els fitxers de configuració per defecte quan es creï un nou usuari. El valor predeterminat és /etc/skel.
*   CREATE\_MAIL\_SPOOL: Si està establert a "yes", es crearà una carpeta de correu per a l'usuari nou. Per defecte, està establert a "yes". ![gestiousunou6](../img/gestiousunou6.png)
*   Aquestes son unes possibles modificacions (d'exemple) ![gestiousunou7](../img/gestiousunou7.png)
    
*   Un altre fitxer que podem modificar es el de la politica de contrasenyes que es aquest `/etc/login.defs`
    
    `[](#__codelineno-42-1)nano /etc/login.defs`
    
    Els parametres que ens permet modificar son:
    
*   MAIL\_DIR: Defineix l'ubicació del directori d'emmagatzematge de correu per als nous usuaris. Per defecte, és /var/mail.
*   PASS\_MAX\_DAYS: Nombre màxim de dies que una contrasenya pot ser vàlida. Per defecte, pot ser 99999, el que significa que no expira mai.
*   PASS\_MIN\_DAYS: Nombre mínim de dies entre canvis de contrasenya. Per defecte, és 0, el que permet canvis immediats.
*   PASS\_MIN\_LEN: Longitud mínima de la contrasenya; no obstant això, en sistemes moderns, aquest paràmetre pot no tenir efecte, ja que la complexitat de la contrasenya es gestiona amb PAM (Pluggable Authentication Modules).
*   PASS\_WARN\_AGE: Nombre de dies abans de l'expiració de la contrasenya que es notifica a l'usuari. Per defecte, és 7.
*   UID\_MIN i UID\_MAX: Rangs mínim i màxim per als identificadors d'usuari (UID) per als nous usuaris. Això ajuda a assegurar que no es creïn usuaris amb UID que podrien entrar en conflicte amb comptes del sistema o altres usuaris.
*   GID\_MIN i GID\_MAX: Rangs mínim i màxim per als identificadors de grup (GID) per als nous grups.
*   CREATE\_HOME: Si està establert a "yes", es crea el directori de casa de l'usuari quan es crea un nou compte; si no, no es crea. Per defecte, pot ser "no" en alguns sistemes per raons de seguretat o per configuracions específiques.
*   ENCRYPT\_METHOD: Mètode de xifrat utilitzat per a les contrasenyes. Pot ser SHA512 o altres mètodes segons la versió del sistema.
*   UMASK: Defineix el valor per defecte de la màscara de permisos per als fitxers creats pels usuaris, afectant els permisos per defecte dels fitxers i directoris.
*   USERGROUPS\_ENAB: Si està establert a "yes", quan un usuari es suprimeix, el seu grup principal també es suprimeix si no hi ha altres membres en aquest grup.

![gestiousunou8](../img/gestiousunou8.png) - Possibles modificacions (d'exemple) ![gestiousunou9](../img/gestiousunou9.png)

Per últim veurem el directori `/etc/skel`, dins d'aquest directori trobarem uns fitxers que son `.bashrc` `.profile` i `.bash_logout`. Aquestos fitxers són scripts de configuració per al shell Bash i Sh que permeten personalitzar l'entorn de l'usuari.

*   Quan es crea un nou usuari amb un directori home, el contingut d'aquest directori /etc/skel es copia al nou directori home de l'usuari. Això permet configurar arxius i directoris per defecte per a tots els nous usuaris.

![gestiousunou10](../img/gestiousunou10.png)

`.bashrc`:

Aquest arxiu s'executa cada vegada que es crea un nou shell interactiu que no és un shell de login (per exemple, quan obres una nova finestra de terminal). Es pot utilitzar per:

*   Definir variables d'entorn: Per a variables que no necessiten ser establertes en el context de login.
    
*   Ajustar alias: Crear atacs ràpids per a comandaments llargs o freqüents.
    
*   Configurar funcions de shell: Afegir funcions personalitzades per facilitar tasques rutinàries.
    
*   Personalitzar el prompt: Canviar l'aparença del prompt del terminal.
    
*   Establir paràmetres de shell: Com historial, compleció de comandaments, etc.
    
*   A continuació un exemple d'us, canviant un "alias". Farem que ll sigui equivalent a la comanda ls -l, així cada cop que posem ll s'executarà un ls -l.
    

![gestiousunou11](../img/gestiousunou11.png) ![gestiousunou12](../img/gestiousunou12.png) ![gestiousunou13](../img/gestiousunou13.png)

`.profile`:

Aquest fitxer s’executa automàticament quan l’usuari inicia sessió. Serveix per definir variables d’entorn i aplicar altres configuracions globals. Alguns exemples d’ús són:

*   Definir variables d’entorn, com PATH.
    
*   Configurar el prompt o ajustar altres opcions del shell.
    
*   Carregar altres fitxers de configuració, com .bashrc, si existeix.
    
*   A continuació un exemple d'us, canviarem l'editor de text per defecte i farem que sigui nano, ja que es el que més utilitzo.
    

![gestiousunou14](../img/gestiousunou14.png) ![gestiousunou15](../img/gestiousunou15.png) ![gestiousunou16](../img/gestiousunou16.png)

`.bash_logout`

Aquest fitxer s’executa de forma automàtica quan l’usuari tanca una sessió interactiva. És especialment útil per a:

*   Alliberar recursos o aturar processos temporals.
    
*   Mostrar missatges de comiat o finalització de sessió.
    
*   Executar scripts personalitzats per tasques de manteniment.
    
*   A continuació configurarem un missatge de sortida.
    

![gestiousunou17](../img/gestiousunou17.png) ![gestiousunou18](../img/gestiousunou18.png) ![gestiousunou19](../img/gestiousunou19.png)

Gestió de permisos
==================

En els casos d'un sistema multiusuari on vulguem que diferents usuaris tinguin certs permisos però no els mateixos, és important fer una bona gestió d'aquestos. Hi han vaires maneres de gestionar-ho, i les veurem a conitnuació.

\- Permisos estandars
---------------------

*   Els permisos estandars son una serie de permisos bàsics que es poden donar a tots els usuaris i grups. Els grups poden tenir diferents permisos respecte als usuaris, una forma de comprovar això ho podem fer de la següent forma.
    
    `[](#__codelineno-43-1)ls -l` 
    
    ![permis](../img/permisbasic.png)
*   En aquest cas podem observar que el primer root que apareix és de l’usuari i el segon és del grup principal. També surt la data de creació i noms de directori, però la part important és al principi. ![permis1](../img/permisbas1.png)
*   Aquí es on podem apreciar els permisos que hi han dins dels directoris. Després de la lletra d, els primers permisos són els d'usuari "rwx" en aquest cas, això vol dir que por llegir, escriure i executar, bàsicament te tots els permisos. Després els següents permisos son els de grup equivalents a les 3 lletres següents: "r-x", en aquest cas com podem veure no te permisos per escriure. I per últim tenim els ultims 3 caràcters que equivalen a altres, usuaris que no són ni usuari principal ni formen part del grup principal, en aquest cas: "r-x", la mateixa situació que abans no poden escriure però si llegir i executar. Aquest exemple es amb "root".
*   A continuació veurem com nosaltres podem agregar permisos als usuaris i grups.
    
    `[](#__codelineno-44-1)chmod -R`
    
*   Opcions de fitxer/carpeta
    
    `[](#__codelineno-45-1)chrgp -R`
    
*   Grup propietari fitxer/carpeta
    
    `[](#__codelineno-46-1)chown - R`
    
*   Propietari fitxer/carpeta.
*   Cada lletra dels permisos te un significat associat: u = usuari, g = grup, o = others, a = all.

\- Permisos especials
---------------------

### \- Sticky

*   L'sticky es un permís d'accés per fitxers i directoris. Quan l'apliquem l'únic usuari que el pot canviar es el root. Es pot aplicar de la següent manera.
    
    `[](#__codelineno-47-1)chmod +t directori`
    
    `[](#__codelineno-48-1)chmod 1775 directori`
    
*   Això es molt útil en sistemes multiusuari ja que sol el root i l'usuari que ha creat cert directori poden borrar o modificar el directori, els altres sol tenen permisos de lectura o escriptura. En cas de voler eliminar l'sticky podem utilitzar la següent comanda.
    
    `[](#__codelineno-49-1)chmod -t directori`
    

### \- sgid

*   sgid es un permís que esta relacionar amb els grups i principalment permet que qualsevol usuari executi l'arxiu com si fos part del grup al que pertany aquell arxiu. Per utilitzar-la podem fer el següent.  
    
    `[](#__codelineno-50-1)chmod g+s`
    

### \- suid

*   suid permet que un arxiu s'executi com si fos el propietari independentment de l'usuari que l'executi. Aquest a diferencia del sgid i sticky no es pot fer un script.
    
    `[](#__codelineno-51-1)chmod g+s` 
    

\- Llistes de control d'accés (ACLs)
------------------------------------

*   Una llista de control d'accés son una serie de regles que ens permeten uns accesos a sistemes de fitxers en aquest cas. Aquestes llistes ens poden donar uns accesos mes restrictius o mes permisius segons la configuarció que faci l'usuari. Per crear una ACL utilitzem la següent comanda.
    
    `[](#__codelineno-52-1)setfacl`
    
    `[](#__codelineno-53-1)setfacl -m user:usuari:rw- exemple.text`
    
    `[](#__codelineno-54-1)setfacl -m group:grup:rwx carpeta`
    
    `[](#__codelineno-55-1)setfacl -b fitxer o carpeta`
    
*   Les restriccions venen donades per les lletres com hem vist abans, utilitza la mateixa nomenclatura. Per comprovar si les restriccions s'han aplicat correctament podem utilitzar la següent comanda.
    
    `[](#__codelineno-56-1)getfacl`
    
    ![acl](../img/acl.png)
    
*   Si ens em equicocat a l'hora de configurar alguna ACL podem eliminar totes les excepcions. (TOTES).
    
    `[](#__codelineno-57-1)setfacl -x usuari carpeta`
    

\- Umask
--------

*   Umask s'utilitza per canviar la mascara del mode de creació d'arxius, auesta determina el valor inicial dels permisos que tindran els arxius que es creein. De forma predeterminada la mascara te el valor dels bits de permís que NO s'han d'establir, per això fem l'operació de negació. Amb les seguents imatges entendrem millor la situació.

![umask2](../img/umask2.png) ![umask](../img/umask.png) - El que esta fetn umask es una operació coneguda com NOR, el que equivaldria a una resta convencional. - Aquestes operacions es poden realitzar amb la següent comanda, tot i que això sol funcionarà temporalment (els arxius ja creats no canvien de permisos).

`[](#__codelineno-58-1)umask + nº`

\- Per a que els canvis siguin permanents tenim que modificar la umask al arxiu que tenim a la següent ruta.

`[](#__codelineno-59-1)/etc/login.defs`

\- Un cop obert l'arxiu modifiquem el valor de la umask per defecte i aquest canvi si que es permantent. ![umask3](../img/umask3.png)

Sistemes de fitxers i particions
================================

\- Estructura de la informació
------------------------------

*   L'estructura de la informació la podem dividir en diverses parts: la física que seria el disc (sòlid o mecànic), i l'estructura lògica que pot ser (gpt o mbr). La part lògica pot ser consultada a través de commandes per la terminal tal i com es mostra a continuació:
    
    `[](#__codelineno-60-1)gdisk /dev/sda`
    
    ![estructura1](../img/estructura1.png)
*   Els discs estan dividits amb blocs i dins de cada bloc tenim uns sectors. El sector és la unitat mínima física on es guarden les dades i per defecte és 512 bytes, però el SO no treballa en sectors treballa en blocs. El bloc és la unitat mínima lògica on es guarden les dades per defecte. La mida del sector no es pot canviar ve definida de fàbrica, però la mida del bloc si es pot canviar. Quan formatem la partició. Per consultar les mides del sector podem utilitzar les seguents comandes.
    
    `[](#__codelineno-61-1)fdisk -l`
    
    ![estructura2](../img/estrucutra2.png) ![estructura3](../img/estructura3.png)
*   Com hem vist també ens surt on es troba instalat el sistema operatiu (part resaltada de l'imatge anterior). Per seguir analitzant les mides de les particions podem utilitzar la següent comanda.
    
    `[](#__codelineno-62-1)tune2fs -l /dev/sda | grep Block`
    
    ![estructura4](../img/estructura4.png)
*   Seguidament si necessitem saber la informació de les particions i sistemes de fitxers que s'utilitzen podem utilitzar aquesta comanda.
    
    `[](#__codelineno-63-1)df -T`
    
    ![estrucutra5](../img/estructura5.png)
*   Les mides dels blocs segons el tipus de fitxers que es guardin ens pot donar problemes, ara veurem dos possibles problemes amb les seves respectives solucions.

### \- Fragmentació interna

La fragmentació interna és l’espai que desaprofitem dels blocs perquè no s’acaben d’emplenar. Una solució possible és canviar la mida del block reduïm la fragmentació interna, però pots fragmentar un arxiu (baixes el rendiment), busquem un equilibri. Aquesta canvi de mida per reduir l'espai del bloc ens pot servir si emmagatzemem arxius que no tinguin una mida molt gran, com podiren ser els fitxers de text. D'altra banda si volem guardar fitxers mes grans com podrien ser pel·licules o ISOs em de fer més gran la mida del bloc perqué sino fragmentarem molt els arxius. RECOMANACIÓ! buscar sempre un equilibri i emmagatzemar els tipus d'arxius diferents en particions diferents, per no barrejar "pelis amb textos".

### \- Fragmentació externa

La fragmentació externa és quan el disc fa temps que treballa i els arxius es guarden en blocs separats i no continus, això ens fa baixar el rendiment, aquesta baixada de rendiment es pot solucionar desfragmentant el disc. La desfragmentació intenta ordenar els arxius per a que no estiguin .

\- Tipus de formateig
---------------------

Hi ha tres maneres de formatar un disc i son les següents.

*   Ràpid: Aquest formateig no borra els arxius, elimina el sistema de fitxers i en cas d'haver-hi un bloc defectuos s'ignora.
    
*   Nivell mig: Aquest tampoc elimina els arxius sinó que elimina el sistema de fitxers igual que ho fa el ràpid, la diferencia es que el mig detecta i marca els sectors i/o blocs defectuosos, sense reperar-los.
    
*   Nivell baix: En aquest igual necessitem algún programa extern. I en aquest cas si es borren els arxius, es borra tot i intenta reparar els blocs defectuosos. És el més lent dels tres. Amb commandes també tal i com es mostra a continuació. Hi ha una command per mostar la cantitat de fragmentació que tenim a la partició en concret (ens recomana si em de desfragmentar o no), i després una altra per desfragmentar-lo.
    
    `[](#__codelineno-64-1)e4defrag -c /dev/sda2 (consulta)`
    
    `[](#__codelineno-65-1)e4defrag /dev/sda2 (desfragmentació)`
    
    ![estructura6](../img/estructura6.png) ![estructura7](../img/estructura7.png)
    

\- Particions
-------------

### \- Creació de particions i formateig

*   En primer lloc per entrar a un disc utilitzem la comanda:
    
    `[](#__codelineno-66-1)fdisk /dev/sdb`
    
*   Aquí assignem la configuració de la partició, en aquest cas seguim amb la configuració per defecte fins al punt de la mida dels sectors, el primer (0-2048) esta reservat per al arrel?, i després assignem l'espai que vulguem. I finalment confirmem la configuració.

![particio1](../img/particio1.png)

*   Amb la comanda de fdisk -l, mirem la configuració que em fet sigui correcte.

![particio2](../img/particio2.png)

*   Per definir la mida del bloc que volem configurar podem utilitzar la següent comanda. Amb aquesta comanda fem la creació d'una partició amb el format d'arxius que vulguem.
    
    `[](#__codelineno-67-1)mkfs.ext4 -b 2048 /dev/sdb1`
    
    ![particio3](../img/particio3.png)
*   Per assegurar-nos de les mides podem utilitzar la següent comanda. ![particio4](../img/particio4.png)

### \- Muntatge

*   Dos opcions: temporal i definitiva:
    
*   Temporal: mount es temporal, un cop montem la partició els fitxers que hi havien abans no apareixen i visceversa. Per comprovar això podem seguir els següents passos crear un arxiu abans del muntatge i un després, així veurem que quan el disc esta muntat sol veiem l'arxiu que em fet mentres aquest estava muntat, en canvi l'arxiu previ sol el podrem visualitzar després de desmuntar-lo, mentres estigui muntat no el veurem. En aquest exemple fem una carpeta "particio1" i dins posem un arxiu "hola".
    

![particio5](../img/particio5.png)

*   Al fer un ls veiem que no ens apareix l'arxiu hola sino un que es diu "lost+found".

![particio6](../img/particio6.png)

*   Després provem de fer un arxiu nou adeu dins la partició i com veiem aquest si ens apareix al fer un ls de la carpeta.

![particio7](../img/particio7.png)

*   Permanent: es al fitxer `/etc/fstab`

![particio8](../img/particio8.png)

En aquest fitxer podem definir els següents parametres:

*   /dev/sdb1: És el dispositiu de bloc que es muntarà.
    
*   /home: És el punt de muntatge, el directori on es muntarà el sistema de fitxers de /dev/sdb1. En aquest cas, es munta a /home.
    
*   ext4: És el tipus de sistema de fitxers que utilitza la partició /dev/sdb1.
    
*   defaults: Són les opcions de muntatge. defaults significa que s'utilitzen les opcions estàndard de muntatge per a ext4.
    
*   0: El primer zero es refereix a l'opció dump, que indica si el sistema de fitxers ha de ser copiat amb dump (un programa de còpia de seguretat). Un valor de 0 significa que no es farà còpia de seguretat automàticament.
    
*   0: El segon zero és per a l'opció pass, que indica l'ordre en què fsck (programa de comprovació i reparació de sistemes de fitxers) ha de ser executat en el sistema de fitxers durant l'inici. Un valor de 0 significa que fsck no es farà automàticament en aquest sistema de fitxers.
    

