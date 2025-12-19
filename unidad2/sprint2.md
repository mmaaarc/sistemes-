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
  
    <img width="806" height="517" alt="image" src="https://github.com/user-attachments/assets/215bf7cf-cf0b-448c-b8c9-eb47789faa99" />

    
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

*   Amb un "top" podem comprovar si ha funcionat correctament.
  
  <img width="1207" height="29" alt="procesos19" src="https://github.com/user-attachments/assets/10a41317-8f8d-4043-84c2-25179f32ca07" />


Gestió d'usuaris grups i permisos
=================================

*   Es important que al nostres sistema tinguem diferents usuaris i que aquestos tinguen diferents caracteristiques, i que els puguem incloure en grups per classificar-los. A més a més, també ens interessarà poder modificar-los, eliminar-los i bloquejar-los al nostre gust. Tot això i més ho veurem a continuació.

\- Commandes terminal i accessos als directoris
-----------------------------------------------

Per a accedir al terminal normalment ho faremt amb un crtl + alt + t, així obrim el pseudo terminal. El terminal com a tal l'obrirem al el ctrl dret + F3, aquest es un terminal TTY. Un pseudo terminal es com un emulador on les comandes que posem son interpretades per algún arxiu al que fan referencia i aquest fa els procediments, en canvi amb un terminal si que estem amb contacte directe amb el sistema.

*   En primer lloc veurem un document que actua com un registre de tots els comptes d'usuaris presents al sistema. Inclou dades com el nom del compte, l'identificador d'usuari (UID), el directori personal i el shell configurat per defecte. Es tracta d'un fitxer públic, cosa que permet que qualsevol pugui consultar qui són els usuaris del sistema.
    
    <img width="1212" height="580" alt="gestiousu1" src="https://github.com/user-attachments/assets/d23bb83f-8d3f-4d99-bda1-853774c7fe34" />

*   A continuació podem veure els grups dels usuaris i l'identificador de qui es el seu administrador.

      <img width="1211" height="720" alt="gestiousu2" src="https://github.com/user-attachments/assets/2df9ea67-4b6e-4a2d-96e4-44d365e7fc70" />

    
*   A continuació, en aquest arxiu es guarda la informació relacionada amb les contrasenyes dels comptes d'usuari. Cada registre fa referència a un usuari i inclou la seva contrasenya codificada. Si apareix el símbol "!", això indica que el compte està deshabilitat i l'usuari no té permís per accedir al sistema.
    
  <img width="1211" height="720" alt="gestiousu3" src="https://github.com/user-attachments/assets/dd4e8d09-8d07-4ac0-883d-03e823be34b4" />
  
*   Per últim aquest arxiu és comparable a /etc/group, però ofereix detalls extres sobre els grups. En aquest lloc es pot identificar qui són els administradors de cada grup. Resulta pràctic per controlar els permisos i gestionar els privilegis d'accés dels diferents grups d'usuaris.
    
    <img width="1211" height="720" alt="gestiousu4" src="https://github.com/user-attachments/assets/b2d4bbc8-22f6-43f2-b71a-cc7721e171af" />


\- Creació d'usuaris
--------------------

Per crear usuaris tenim diverses formes de fer-ho, el més important es tenir clar que amb certes comandes no es creen directoris sol usuaris. A continuació es mostrarà com crear usuaris.

*   En primer lloc utilitzarem la següent comanda, aquesta ens creara un usuari pero fins que no fessim un log in amb aquest no ens crearà els directoris. Aquesta es la forma més senzilla de crear els usuaris ja que et ve pautada pel propi sistema operatiu.
  
<img width="1211" height="720" alt="gestiousu5" src="https://github.com/user-attachments/assets/4b36b735-3c79-4881-83b8-e884a2fa1aca" />


Per crear un nou compte d'usuari al sistema, farem servir la comanda useradd. Aquesta comanda ens permetrà afegir usuaris al sistema amb diversos paràmetres que ens ajuden a configurar les seves propietats. A continuació, detallem alguns dels paràmetres més destacats que podem utilitzar:
    
*   \-m: Indica que es generarà automàticament un directori personal per a l'usuari.
    
*   \-s /bin/bash: Aquest paràmetre ens permet definir el shell per defecte de l'usuari.
    
*   \-d /home/alumne2: Amb aquest paràmetre, especifiquem el directori inicial de l'usuari. Per exemple, en aquest cas, el directori personal serà /home/alumne2.
    
*   alumne2: Correspon al nom de l'usuari que estem creant. En aquest exemple, l'usuari es dirà "alumne2".
    
*   && passwd alumne2: Aquesta comanda s’utilitza per assignar o modificar la contrasenya de l’usuari "alumne".
    

<img width="1089" height="31" alt="gestiousu6" src="https://github.com/user-attachments/assets/eb070f06-729d-45f2-a18c-d229337cd1c1" />

- Sino utilitzem la comanda -m per als directoris els podem afegir de la següetn manera.

<img width="1213" height="728" alt="gestiousu8" src="https://github.com/user-attachments/assets/548e1a70-b290-4279-9496-3e16c9a4950c" />

*   Si volem canviar el nom de l'usuari podem utilitzar la següent comanda. EN el cas que hi ha a continuació volem canviar el nom d'usuari de porva2, ja que hauria de ser prova2.

<img width="721" height="49" alt="gestiousu15" src="https://github.com/user-attachments/assets/7385f45b-dce6-4120-87d6-0142f5cdc274" />

<img width="721" height="49" alt="gestiousu16" src="https://github.com/user-attachments/assets/d52d9e61-83e2-4345-8d5e-d31d20ade4db" />



*   En cas de voler eliminar accés a un usari ho podem fer bloquejant-lo, la comanda seria la següent. Una forma de comprovar que s'ha bloquejat correctament es entrar a la carpeta de passwd i veurem que la contrasenya del usuari al davant té un signe d'exclamació "!"

<img width="1213" height="26" alt="gestiousu9" src="https://github.com/user-attachments/assets/f12ad2ef-0b87-4053-8e79-29517ddb6f54" />

<img width="1213" height="591" alt="gestiousu10" src="https://github.com/user-attachments/assets/9d5bd325-2aba-4974-9407-0937df9fa434" />

- Seguint amb la creació d'usuaris, si tenim un usuari bloquejat i el volem recuperar utilitzarem aquesta comanda. A l'hora de comprovar-ho ens fixarem que ja no te l'exclamació.

<img width="1213" height="718" alt="gestiousu13" src="https://github.com/user-attachments/assets/4c152dee-42ab-467a-a932-754886469ec7" />


- Si realment el que volem es eliminar l'usuari de forma més permanent ho farem amb la següent comanda. Per comprovar si l'hem eliminat correctament podem entrar a la carpeta passwd i veurem que l'usuari ja no hi es.

`[](#__codelineno-28-1)deluser usuari`

<img width="1213" height="98" alt="gestiousu11" src="https://github.com/user-attachments/assets/039668ec-68df-4efd-b48b-f8e03669bced" />

<img width="1213" height="718" alt="gestiousu12" src="https://github.com/user-attachments/assets/6a2ecf2d-7c39-48f3-abe0-6f591e891579" />

 
*   En cas de voler consultar algun tipus d'informació sobre algun usuari, podem fer-ho així.
  
 <img width="1212" height="223" alt="gestiousu18" src="https://github.com/user-attachments/assets/4c6cca96-9895-46a4-bb4c-c9846fb70c4a" />
   
    
*   Un cop vist com es el funcionament a través del terminal podrem observar com es fa per l'interficie gràfica d'Ubuntu. Dins de la configuració de sistema hem d'entrar a l'apartat usuaris, i després seguirem els passos que hi ha a continuació.
*

*   <img width="1214" height="770" alt="gestiousunou1" src="https://github.com/user-attachments/assets/911eb5d0-b1ba-488a-bb72-7dcd6f7270e4" />

*<img width="1214" height="71" alt="gestiousunou2" src="https://github.com/user-attachments/assets/cc0d32df-f2f5-4fce-98ab-e503955f2b41" />

*<img width="1214" height="704" alt="gestiousunou3" src="https://github.com/user-attachments/assets/51857bcc-5d9b-401e-9ed7-5f68f128d39d" />

*<img width="1214" height="768" alt="gestiousunou4" src="https://github.com/user-attachments/assets/2ac38f68-b752-496a-a097-ab6b6607e4e8" />

<img width="1214" height="768" alt="gestiousunou5" src="https://github.com/user-attachments/assets/a600484b-9d25-45df-9367-4dc3312a565e" />


\- Creació de grups
-------------------

*   En aquest apartat veurem com funcionen els grups d'usuaris, com hem vist anteriorment podem consultar els grups i les seves contrasenyes. Important dir que quan es crea un usuari també es crea un grup amb el nom d'aquest.
*   Per crear un grup nou ho podem fer amb una senzilla comanda.

     <img width="1213" height="170" alt="gestiogrup" src="https://github.com/user-attachments/assets/a1fcd813-6cff-4a72-844c-f535f54a7a88" />
     
<img width="1213" height="714" alt="gestiogrup1" src="https://github.com/user-attachments/assets/418a4288-c902-4f15-9c3e-e82a977bb3aa" />

    
*   D'altra banda si el que volem es afegir un usuari a un grup existent ho podem fer d'aquesta manera.
    
    <img width="1213" height="93" alt="gestiogrup2" src="https://github.com/user-attachments/assets/9c174a94-bb9f-4368-a66d-aa43f65a063a" />

<img width="1213" height="93" alt="gestiogrup3" src="https://github.com/user-attachments/assets/26e761d3-e20c-4bd3-b80b-6a1927af0fd1" />

        
*   Per fer a un usuari administrador d'aquell grup ho podem fer així. Dins de la carpeta gshadow podem veure els usuaris i administradors dels grups, per reconeixels veurem la posició que tenen entre els ":", l'alumne 2 es administrador d'asix1 i membre d'asix2.
*   
     <img width="1221" height="71" alt="gestiogrup4" src="https://github.com/user-attachments/assets/376246e4-4a77-4e95-ac9a-333ba3222e07" />

    <img width="1221" height="636" alt="gestiogrup5" src="https://github.com/user-attachments/assets/25c71f85-31b9-4c92-ba80-bf959b2437e3" />

    
*   Un dels majors problemes es que quan afegim usuaris a grups amb les comandes anteriors els treu del grup on estaven, per evitar-ho hem d'utilitzar la següent comanda. Com comprovarem l'usuari alumne2 forma part dels dos grups d'asix i es administrador del primer.
    
    <img width="1221" height="64" alt="gestiogrup6" src="https://github.com/user-attachments/assets/943f8804-056c-4c79-b2fe-3aad995b19e6" />

<img width="1221" height="64" alt="gestiogrup7" src="https://github.com/user-attachments/assets/fe556799-ad48-448c-8c02-c148596aa8b8" />

    
*   Per eliminar un usuari d'un grup ho farem com veurem a continuació. En aquest cas l'alumne2 ja te prous responsabilitats i l'eliminarem del grup d'asix1.
    
    <img width="1221" height="78" alt="gestiogrups8" src="https://github.com/user-attachments/assets/1e646ff4-81c1-40db-a053-abd0baec0ac4" />

<img width="1221" height="643" alt="gestiogrup9" src="https://github.com/user-attachments/assets/a2107e97-f40f-4b8f-a119-08f4edfd1877" />

    
*   L'anterior comanda també es pot fer amb aquesta altra
    
    <img width="1221" height="95" alt="gestiogrup10" src="https://github.com/user-attachments/assets/1d9f44ea-686f-46c9-966b-84cbf6407f56" />

    
*   Per fer un usuari el principal d'un grup en concret utilitzarem el següent.
    
    `[](#__codelineno-39-1)usermod -g grup usuari`
    
*   En cas de voler canviar el nom d'algun grup ho farem amb la següent comanda.
  
    <img width="1221" height="47" alt="gestiogrup11" src="https://github.com/user-attachments/assets/63288eeb-bb01-4128-829e-d68fda365738" />

    <img width="1221" height="648" alt="gestiogrup12" src="https://github.com/user-attachments/assets/ed9761c4-a05b-4b68-b03f-0b4463e482b6" />


\- Configuració de fitxers d'usuari
-----------------------------------

Gestió de permisos
==================

En els casos d'un sistema multiusuari on vulguem que diferents usuaris tinguin certs permisos però no els mateixos, és important fer una bona gestió d'aquestos. Hi han vaires maneres de gestionar-ho, i les veurem a conitnuació.

\- Permisos estandars
---------------------

*   Els permisos estandars son una serie de permisos bàsics que es poden donar a tots els usuaris i grups. Els grups poden tenir diferents permisos respecte als usuaris, una forma de comprovar això ho podem fer de la següent forma.
    
 <img width="623" height="239" alt="permisbasic" src="https://github.com/user-attachments/assets/fb0e3317-4a01-4e0b-9b6e-7be37e86b2ef" />
   
*   En aquest cas podem observar que el primer root que apareix és de l’usuari i el segon és del grup principal. També surt la data de creació i noms de directori, però la part important és al principi. ![permis1](../img/permisbas1.png)
*   Aquí es on podem apreciar els permisos que hi han dins dels directoris. Després de la lletra d, els primers permisos són els d'usuari "rwx" en aquest cas, això vol dir que por llegir, escriure i executar, bàsicament te tots els permisos. Després els següents permisos son els de grup equivalents a les 3 lletres següents: "r-x", en aquest cas com podem veure no te permisos per escriure. I per últim tenim els ultims 3 caràcters que equivalen a altres, usuaris que no són ni usuari principal ni formen part del grup principal, en aquest cas: "r-x", la mateixa situació que abans no poden escriure però si llegir i executar. Aquest exemple es amb "root".
*   A continuació veurem com nosaltres podem agregar permisos als usuaris i grups.

  D'aquesta manera faig propietari de la carpeta cire a cire.
    
<img width="438" height="74" alt="image" src="https://github.com/user-attachments/assets/6d457e01-774c-4da9-89dd-d6c2c06ada47" />

<img width="542" height="63" alt="image" src="https://github.com/user-attachments/assets/8bd4d361-e6b3-4b75-a5f4-62f26dd7af74" />

    
*   Opcions de fitxer/carpeta

  Amb aquesta opció canvio el grup de la carpeta cire al grup cire.
    
<img width="439" height="62" alt="image" src="https://github.com/user-attachments/assets/2e4028b2-ab6f-40bf-acba-83e6882e7b2c" />

I puc comprovar que ara ja forma part del usuair cire i del grup cire.
<img width="489" height="72" alt="image" src="https://github.com/user-attachments/assets/c42be974-277f-4651-9872-85601f3e041e" />


    
*   Grup propietari fitxer/carpeta

 També podem feru a la vegada on podrem canviar l'usuari i el grup de la carpeta i de tots els fitxers que tingue.

<img width="581" height="134" alt="image" src="https://github.com/user-attachments/assets/022cf7fe-20ec-4ff3-b2a3-ef4b1325db11" />

    
*   Propietari fitxer/carpeta.
*   Cada lletra dels permisos te un significat associat: u = usuari, g = grup, o = others, a = all.

\- Permisos especials
---------------------

### \- Sticky

*   L'sticky es un permís d'accés per fitxers i directoris. Quan l'apliquem l'únic usuari que el pot canviar es el propietari. Es pot aplicar de la següent manera.
    
<img width="497" height="116" alt="image" src="https://github.com/user-attachments/assets/9934016a-f588-40f1-b4ab-61ec11cfa7ef" />
    
Això a l'hora de veure els permísos ens sortira una t informan de que em afegit aquest permís on unicament el porpietari podra eliminar la carpeta o modificar-la.

<img width="572" height="56" alt="image" src="https://github.com/user-attachments/assets/39e56fd0-d23b-4c20-aa08-c86c4a321533" />

*   Això es molt útil en sistemes multiusuari ja que sol el root i l'usuari que ha creat cert directori poden borrar o modificar el directori, els altres sol tenen permisos de lectura o escriptura. En cas de voler eliminar l'sticky podem utilitzar la següent comanda.
    
<img width="377" height="58" alt="image" src="https://github.com/user-attachments/assets/b06250ea-2e85-42c4-acb7-3dbd5e59f599" />
    

### \- sgid

*   sgid es un permís que esta relacionar amb els grups i principalment permet que qualsevol usuari executi l'arxiu com si fos part del grup al que pertany aquell arxiu. Per utilitzar-la podem fer el següent.  
    
D'aquesta manera aplico el permís sguid.

<img width="382" height="70" alt="image" src="https://github.com/user-attachments/assets/820fd185-5e48-465e-b3cc-f370fc4fadf6" />

Si ara desde un altre usuari com marc creo un arxiu a dins del directori cire aquest agafara el grup del directori no del usuari creat.

<img width="660" height="52" alt="image" src="https://github.com/user-attachments/assets/a0ab8f27-496a-439b-b582-6c80511b0d6a" />


### \- suid

*   suid permet que un arxiu s'executi com si fos el propietari independentment de l'usuari que l'executi. Aquest a diferencia del sgid i sticky no es pot fer un script.
    
    `[](#__codelineno-51-1)chmod g+s` 
    

\- Llistes de control d'accés (ACLs)
------------------------------------

*   Una llista de control d'accés son una serie de regles que ens permeten uns accesos a sistemes de fitxers en aquest cas. Aquestes llistes ens poden donar uns accesos mes restrictius o mes permisius segons la configuarció que faci l'usuari. Per crear una ACL utilitzem la següent comanda.
    
Ara fare la practica en un grup on primer aplico la acl.

<img width="480" height="217" alt="image" src="https://github.com/user-attachments/assets/a16dc818-9df5-46ad-babb-d2da491e75fb" />

Amb aquest comanda podem veure les llistes de control d'accés aplicades en un fitxer o directori.

<img width="349" height="125" alt="image" src="https://github.com/user-attachments/assets/8f2cd0b6-43f4-4d02-8275-e900b98231c5" />

He fet la prova per l'usuari segon sobre la carpeta numero on aques usuari no tindra cap permís ni escritura ni lectura ni execució.

<img width="498" height="47" alt="image" src="https://github.com/user-attachments/assets/04bd1954-a6ef-4227-8a75-ad77ada5a338" />

Ara torno a llistar les llistes d'ACLs i ens mostra la que hem creat per l'usuari segon.

<img width="343" height="158" alt="image" src="https://github.com/user-attachments/assets/a36759e9-bca4-41d9-b9ab-4ca1da3709c4" />

I seguidament faig la prova on root podra crear arxius i modificarlos i l'usuari segon no podra fer cap acció.

<img width="471" height="227" alt="image" src="https://github.com/user-attachments/assets/4aa618c9-019e-4d4d-9c17-4f07757bf81d" />


\- Umask
--------

*   Umask s'utilitza per canviar la mascara del mode de creació d'arxius, auqesta determina el valor inicial dels permisos que tindran els arxius que es creein. De forma predeterminada la mascara te el valor dels bits de permís que NO s'han d'establir, per això fem l'operació de negació. Amb les seguents imatges entendrem millor la situació.

Primer li aplico la umask, per fer la prova li aplico la 027, per tant els permisos que s'afegiran al crear un arxiu seran 640, ja que es resta 777 - 027.

<img width="332" height="50" alt="image" src="https://github.com/user-attachments/assets/c88fbc7e-bd1c-442e-8c2f-2d743f394e9c" />

Ara creo un arxiu.

<img width="339" height="37" alt="image" src="https://github.com/user-attachments/assets/f7809532-7d7c-48ec-87f3-a01c66ccc16a" />

Finalment comprovo que els permisos s'han aplicat amb 640.

<img width="613" height="58" alt="image" src="https://github.com/user-attachments/assets/9efd005a-516a-4286-9567-fc6bd16f7d19" />

Per aplicar la umask per sempre i no per la sessió actual s'afegeix en aquest arxiu al final.

<img width="705" height="513" alt="image" src="https://github.com/user-attachments/assets/60283044-992a-458e-80a0-8cac398ffd8d" />


Sistemes de fitxers i particions
================================

\- Estructura de la informació
------------------------------

*   L'estructura de la informació la podem dividir en diverses parts: la física que seria el disc (sòlid o mecànic), i l'estructura lògica que pot ser (gpt o mbr). La part lògica pot ser consultada a través de commandes per la terminal tal i com es mostra a continuació:
    
  <img width="1218" height="329" alt="estructura1" src="https://github.com/user-attachments/assets/7a4d382e-6ea4-46e0-83fd-2e06b3c999d6" />

*   Els discs estan dividits amb blocs i dins de cada bloc tenim uns sectors. El sector és la unitat mínima física on es guarden les dades i per defecte és 512 bytes, però el SO no treballa en sectors treballa en blocs. El bloc és la unitat mínima lògica on es guarden les dades per defecte. La mida del sector no es pot canviar ve definida de fàbrica, però la mida del bloc si es pot canviar. Quan formatem la partició. Per consultar les mides del sector podem utilitzar les seguents comandes.
    
    <img width="1222" height="648" alt="estructura3" src="https://github.com/user-attachments/assets/2d120054-219d-43ec-84d7-ef46f01d9e97" />

*   Com hem vist també ens surt on es troba instalat el sistema operatiu (part resaltada de l'imatge anterior). Per seguir analitzant les mides de les particions podem utilitzar la següent comanda.
  
    <img width="1210" height="97" alt="estructura4" src="https://github.com/user-attachments/assets/9ebdf43f-0be8-4719-baf2-1d72cffc8429" />

    
*   Seguidament si necessitem saber la informació de les particions i sistemes de fitxers que s'utilitzen podem utilitzar aquesta comanda.
    
    <img width="1210" height="157" alt="estructura5" src="https://github.com/user-attachments/assets/021db590-85fc-4be2-bf7e-33e25b59e410" />

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
    
    
    <img width="1208" height="334" alt="estructura6" src="https://github.com/user-attachments/assets/686403c1-68e1-4e01-87c8-3e08954b2804" />

    <img width="1205" height="710" alt="estructura7" src="https://github.com/user-attachments/assets/653001d8-3033-4340-b34a-db3d3bcb4b35" />


\- Particions
-------------

### \- Creació de particions i formateig

*   En primer lloc per entrar a un disc utilitzem la comanda:
    
    fdisk /dev/sdb
    
*   Aquí assignem la configuració de la partició, en aquest cas seguim amb la configuració per defecte fins al punt de la mida dels sectors, el primer (0-2048) esta reservat per al arrel?, i després assignem l'espai que vulguem. I finalment confirmem la configuració.
   
<img width="889" height="626" alt="particio1" src="https://github.com/user-attachments/assets/bb2bac5b-cc6b-4121-8d6c-c16781271314" />


*   Amb la comanda de fdisk -l, mirem la configuració que em fet sigui correcte.
  
<img width="1218" height="261" alt="particio2" src="https://github.com/user-attachments/assets/9416e5f6-7e29-4be0-9b6f-385137338067" />


*   Per definir la mida del bloc que volem configurar podem utilitzar la següent comanda. Amb aquesta comanda fem la creació d'una partició amb el format d'arxius que vulguem.
    
 <img width="1218" height="296" alt="particio3" src="https://github.com/user-attachments/assets/845d4fcd-d452-4a70-9325-21ab0abe34c6" />
   
*   Per assegurar-nos de les mides podem utilitzar la següent comanda. ![particio4](../img/particio4.png)

### \- Muntatge

*   Dos opcions: temporal i definitiva:
    
*   Temporal: mount es temporal, un cop montem la partició els fitxers que hi havien abans no apareixen i visceversa. Per comprovar això podem seguir els següents passos crear un arxiu abans del muntatge i un després, així veurem que quan el disc esta muntat sol veiem l'arxiu que em fet mentres aquest estava muntat, en canvi l'arxiu previ sol el podrem visualitzar després de desmuntar-lo, mentres estigui muntat no el veurem. En aquest exemple fem una carpeta "particio1" i dins posem un arxiu "hola".
    
<img width="1219" height="378" alt="particio5" src="https://github.com/user-attachments/assets/82590cb4-ff22-451b-8502-0ec22ea4a0e5" />


*   Al fer un ls veiem que no ens apareix l'arxiu hola sino un que es diu "lost+found".
  
<img width="1219" height="602" alt="particio6" src="https://github.com/user-attachments/assets/d5138754-3d01-442a-8096-ef68bc61dfe7" />


*   Després provem de fer un arxiu nou adeu dins la partició i com veiem aquest si ens apareix al fer un ls de la carpeta.

<img width="1209" height="73" alt="particio7" src="https://github.com/user-attachments/assets/a4fce79b-0cf1-4fa1-91a4-ce0a28beef7f" />


*   Permanent: es al fitxer `/etc/fstab`

<img width="1219" height="602" alt="particio8" src="https://github.com/user-attachments/assets/8092c66d-1cd5-491d-8521-da5af88b893d" />

En aquest fitxer podem definir els següents parametres:

*   /dev/sdb1: És el dispositiu de bloc que es muntarà.
    
*   /home: És el punt de muntatge, el directori on es muntarà el sistema de fitxers de /dev/sdb1. En aquest cas, es munta a /home.
    
*   ext4: És el tipus de sistema de fitxers que utilitza la partició /dev/sdb1.
    
*   defaults: Són les opcions de muntatge. defaults significa que s'utilitzen les opcions estàndard de muntatge per a ext4.
    
*   0: El primer zero es refereix a l'opció dump, que indica si el sistema de fitxers ha de ser copiat amb dump (un programa de còpia de seguretat). Un valor de 0 significa que no es farà còpia de seguretat automàticament.
    
*   0: El segon zero és per a l'opció pass, que indica l'ordre en què fsck (programa de comprovació i reparació de sistemes de fitxers) ha de ser executat en el sistema de fitxers durant l'inici. Un valor de 0 significa que fsck no es farà automàticament en aquest sistema de fitxers.
    
Copia de seguretat i automatització de tasques
==============================================

Teoria
------

Hi han tres tipus de copies: completes, diferencials, incrementals. Bona politica de copies, bona gestió dels tipus.

*   Completa: Sempre que es pugui fer una copia completa, (buscar teoria, ventatga principal, desaventatge principal, i quina hem de recuperar).
    
*   Diferencials: copia la diferencia de la completa, sempre de la última, es més rapida. Pero per a recuperar-la sempre fan falta tant l'última completa com l'última diferencial, ocupa menys espai.
    
*   Incremental: Copia la diferencia de la completa, després però sol copia l'anterior incremental, hauries de recuperar totes les incrementals. Menys espai, per recuperar farira falta l'última completa i totes les incrementals.
    

Programes (sol 1 opció)
-----------------------

### Deja-dup (opcional)

### Duplicity

Comandes
--------

### Explicació i taula comparativa

### cp

*   És una copia simple no intel·ligent. Copia tot sense miraments sol funciona en local.

### rsync

*   Es una copia intel·ligent sol copia els fitxers modificats, copies entre maquines utilitzant ssh.

### dd

*   No es per fer copies de fitxers / arxius, sino a nivell particions i disc, es com una clonació. Treballa a nivell local i copia tot, no es intel·ligent. També serveix per sobrescriure dades sector a sector, diferent a formatar, dona seguretat per no recuperar les dades previes, esborra tot a nivell de bloc.

Automatització amb scripts, cron i anacron
------------------------------------------

### Diferencies entre anacron i cron

Cron:

*   Funció: Automatitza tasques específiques en moments precisos (hora, dia, mes, etc.).
*   Ús: És útil quan vols que una tasca s'executi a una hora concreta, per exemple, cada dia a les 2:00 AM.
*   Limitació: Només funciona quan l'ordinador està encès; si està apagat en el moment programat, la tasca no s'executarà.

Anacron:

*   Funció: També automatitza tasques, però està dissenyat per a màquines que no estan sempre enceses.
*   Ús: Ideal per a tasques de manteniment del sistema que no depenen de l'hora exacta, com actualitzacions periòdiques. Quan engeguem l'ordinador, anacron comprova si hi ha tasques pendents i les executa.
*   Avantatge: Funciona bé en ordinadors que es tanquen sovint, ja que no es perd cap tasca programada.

Cron: Per tasques específiques per a un usuari o quan necessites precisió temporal (per exemple, backups diaris a una hora concreta).

Anacron: Per tasques generals, com manteniment del sistema que no requereixen ser executades en un moment exacte.

Configuració de cron:

*   Arxiu global: `/etc/crontab` per tasques que afecten tots els usuaris.
*   Usuari específic: Utilitza crontab -e -u usuari per configurar tasques per a un usuari particular.
*   Carpetes predeterminades: Dins de `/etc/cron.daily/`, `/etc/cron.monthly/`, i `/etc/cron.annually/` per scripts que s'executin diàriament, mensualment o anualment, respectivament.

Configuració de anacron:

*   Arxiu: `/etc/anacrontab` on es defineixen les tasques d'anacron.

<img width="477" height="142" alt="image" src="https://github.com/user-attachments/assets/82bcf1d7-8807-435a-80cf-0dc5555e44af" />

### Exemple d'un script

*   Per preparar un script primer crearem els directoris que volem copiar, que es troben dins del directori Imatges.

<img width="623" height="104" alt="image" src="https://github.com/user-attachments/assets/ec50567a-2a45-4adb-bfed-80898f407cdf" />

*   En primer lloc crearem un script que crea una copia comprimida del directori /home/alumnat/Imatges/ i el desa a l'escriptori amb un nom que inclou la data i hora actuals.

<img width="609" height="127" alt="image" src="https://github.com/user-attachments/assets/754f35db-4566-4525-9ead-2b81de9b0692" />

*   A continuació dins del fitxer crontab, afegim la ruta del nostre script. Com es pot verue a la següent imatge li definim el minut hora i dia del mes, i amb un \* a l'apartat dels dies per a que es faci cada dia.

<img width="753" height="356" alt="image" src="https://github.com/user-attachments/assets/7185d014-cb93-4e38-8231-d501ce504023" />

*   Per comprovar el seu funcionament esperem fins l'hora que em designat, com es veu a la següent imatge es crea l'arxiu comprimit, al descomprimir-lo podem veure que si ha fet la copia dels dos directoris que hi ha a la carpeta Imatges.

<img width="748" height="352" alt="image" src="https://github.com/user-attachments/assets/a11cac4c-5fe6-48aa-9dc6-83083e17f091" />

*   A continuació deixem la linea del crontab comentada. I seguidament del nostre escript li traurem el punt sh i el mourem a la carpeta de cron.daily.

<img width="754" height="342" alt="image" src="https://github.com/user-attachments/assets/0876464b-819f-468e-b195-167051cc11a3" />
<img width="683" height="223" alt="image" src="https://github.com/user-attachments/assets/6e232b62-965f-4da1-af16-403107473348" />
<img width="719" height="108" alt="image" src="https://github.com/user-attachments/assets/74d51513-5033-42e3-8f93-5f61e6fb8dba" />


*   Per assegurar que l'script s'executi al obrir l'ordinador, obrim el fitxer `/var/spool/anacron/cron.daily`, aquí s'indica l'última vegada que es van executar les tasques diàries. En aquest cas ens interessa que no hi hagui res.

<img width="759" height="111" alt="image" src="https://github.com/user-attachments/assets/83c01aa8-d993-42c9-a292-a3eab5ec1bf1" />

*   Amb l'script al lloc de les tasques diaries i amb la comprovació de que no s'han realitzat encara obrim `/etc/anacrontab` i el configurem tal i com es mostra a continuació. Posem que s'executin en 1 minut després de l'arrencada del dispositiu.

<img width="755" height="200" alt="image" src="https://github.com/user-attachments/assets/9c9edaec-2431-4d89-aaba-dee9757cf6c6" />

*   Un cop reiniciat l'ordinador esperem un minut i veurem que a l'escriptori apareix la copia del directori imatges, i si mirem el cron.daily veurem que s'ha executat la tasca diaria.

<img width="760" height="461" alt="image" src="https://github.com/user-attachments/assets/c0003167-3596-4781-927b-2bdad20c237a" />

<img width="758" height="392" alt="image" src="https://github.com/user-attachments/assets/5fff0aa2-2eb5-4b04-87bb-71f619a6c6bf" />

Quotes de disc
==============

Les quotes de disc són unes limitacions imposades a l'ús d'emmagatzematge d'un sistema en aquest cas cas Ubuntu. És poden limitar tant per usuaris com per grups, això es fa per optimitzar l'espai i no fer un malbaratament d'espai. Les quotes es poden modificar en entorns de servidors o ordinadors multiusuari, i els limets pot ser tant de mida com de número de fitxers.

*   En aquest cas assignarem un disc nou de 5GB per fer proves, com hem vist en passos anteriors fem una partició nova amb tot l'espai del disc i format d'arxius ext4.

<img width="759" height="144" alt="image" src="https://github.com/user-attachments/assets/8ff55f05-044d-4aba-8e79-d1a4062ce011" />

*   Per configurar les quotes de disc haurem d'instal·lar quota.
    
    `[](#__codelineno-72-1)sudo apt update`
    
    `[](#__codelineno-73-1)sudo apt install quota`
    
<img width="727" height="312" alt="image" src="https://github.com/user-attachments/assets/49d81f4f-1df8-459c-9ac9-e22fc129018d" />
    
*   Per fer les proves crearem una carpeta "dades"
    

<img width="756" height="52" alt="image" src="https://github.com/user-attachments/assets/710e8b46-98ef-4e80-ae98-0edbd45c6caf" />

*   En aquest punt ens interessarà fer un muntatge permanent i posar les quotes a l'arxiu fstab. Aplicarem quotes d'usuari i de grup. ![quota4](../quota4.png)
    
*   A continuació, farem un reinici del sistema i comprovarem el muntatge i afegirem els fitxers de les quotes d'usuari i de grup, i també les activarem. Per provar les quotes assignarem un usuari nou anomenat usuari5. Finalment amb un ls comprovarem que els canvis s'hagin aplicat.
    
    `[](#__codelineno-74-1)quotacheck -cug /mnt/dades`
    
    `[](#__codelineno-75-1)quotaon /mnt/dades`
    
<img width="724" height="67" alt="image" src="https://github.com/user-attachments/assets/4a25555f-4753-4b9d-b8b7-5944d06f2b10" />
    
*   Per veure les quotes assignades a l'usuari5 podem comprovar-ho de la següent forma. ![quota6](../img/quota6.png)
    
*   Com podem veure encara no te cap quota assignada, per fer-ho podem utilitzar la següent comanda.
    
    `[](#__codelineno-76-1)edquota -u usuari5`
    
 <img width="727" height="45" alt="image" src="https://github.com/user-attachments/assets/c5c907f0-622f-4674-954c-22d7fc917acd" />

    L'arxiu que modificarem conté aquests parametres:
    
*   Filesystem (/dev/sdc1): Aquest és el sistema de fitxers o partició del disc on s'apliquen les quotes.
    
*   blocks: Representa l'espai en disc actualment utilitzat per l'usuari en blocs.
    
*   soft: 1024 és el límit "soft" d'espai en blocs que l'usuari pot utilitzar. Aquest límit pot ser excedit temporalment, però es recomana no sobrepassar-lo.
    
*   hard: 2048 és el límit "hard" d'espai en blocs. Aquest límit no es pot excedir. Si l'usuari intenta utilitzar més espai del que li correspon per aquest límit, no podrà guardar més dades.
    
*   inodes:Representa el nombre d'inodes (estructures de dades que representen fitxers) actualment utilitzats per l'usuari.
    
*   soft: És el límit "soft" per al nombre d'inodes. No està establert en aquest cas, indicant que no hi ha límit soft per al nombre de fitxers.
    
*   hard: És el límit "hard" per al nombre d'inodes. Com amb el límit soft, no està establert.
    

Seguidament accedirem a l'usuari 5 i modificarem els permisos també afegirem una comanda on pasarà el següent: dd: Es crea un fitxer anomenat test amb dades de /dev/zero de 800 KiB (bs=1K count=800).

`[](#__codelineno-77-1)dd if=/dev/zero of=test bs=1K count=800`

\- Per veure un informe detallat del disc i les seves quotes utilitzarem la següent comanmda:

`[](#__codelineno-78-1)repquota /dev/sdc1`

<img width="749" height="400" alt="image" src="https://github.com/user-attachments/assets/4deb80a2-1845-45dd-833f-4a65b6ffe9c8" />

*   Continuant amb les proves generarem un altre arxiu test per comprovar que passa si superem la cantitat d'emmagatzematge assignada. ![quota9](../img/quota9.png)
    
    `[](#__codelineno-79-1)s'ha execedit la quota de disc`

    <img width="721" height="272" alt="image" src="https://github.com/user-attachments/assets/fc1f9025-6f2c-4107-90b9-b5a569355a84" />

    
*   Una vegada mes podem utilitzar la comanda `quota -u usuari5` per comprovar els següents parametres.

  <img width="724" height="64" alt="image" src="https://github.com/user-attachments/assets/d246d18b-05d8-43e6-b7be-33a5944b4c19" />

    
*   Per acabar també podem modificar els dies de gràcia per defecte.
    
    edquota -t`
    
<img width="723" height="74" alt="image" src="https://github.com/user-attachments/assets/8268577f-f410-4178-bb8c-3a54312f8aa8" />

