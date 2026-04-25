---
layout: default
title: Sprint1Windows
---

# Sprint1Windows

## Qu?? ??s Windows Server?
Windows Server ??s un sistema operatiu desenvolupat per Microsoft dissenyat per a la gesti?? de servidors. A difer??ncia de les versions d'escriptori de Windows, est?? optimitzat per oferir serveis de xarxa, allotjament de bases de dades, administraci?? d'usuaris, gesti?? de dominis, i altres funcions cr??tiques per a entorns empresarials i corporatius.

[Lic??ncies de windows.](https://chaminita94.github.io/mkdocs/licenciawind/)

### Per a qu?? s'utilitza?
Windows Server s'utilitza en empreses i entorns professionals per proporcionar serveis com:
- Control de dominis amb Active Directory
- Servidor de fitxers i impressi??
- Serveis web (IIS)
- Virtualitzaci?? amb Hyper-V
- Allotjament de bases de dades
- Administraci?? de xarxes i seguretat

### Cost i llic??ncia
Windows Server no ??s un sistema operatiu gratu??t. Microsoft ofereix diferents edicions amb llic??ncies de pagament segons les necessitats de l'empresa. Existeixen edicions com Standard, Datacenter i Essentials, cadascuna amb caracter??stiques i preus diferents. No obstant aix??, es pot obtenir una versi?? de prova limitada en temps per a proves i aprenentatge.

## Instal??laci?? de Windows Server en VirtualBox
Aquest apartat explica els passos per instal??lar Windows Server en una m??quina virtual amb VirtualBox.

**Creaci?? de la M??quina Virtual**
- Feu clic a "New" per comen??ar la creaci?? de la m??quina virtual.
- Afegiu el nom a la m??quina virtual.
- Inseriu la ISO de Windows Server.
- Feu clic a "Skip unattended installation" per procedir amb una instal??laci?? manual.

![Captura de la pantalla de creaci?? de la m??quina](https://chaminita94.github.io/mkdocs/custom/serviso.png)

**Configuraci?? de Recursos**
- Escolliu la quantitat de RAM i les CPU virtuals o threads que assignareu a la m??quina.
- Deixeu les altres opcions amb els valors per defecte.

![Configuraci?? de la RAM i CPU](https://chaminita94.github.io/mkdocs/custom/RAM.png)

**Inici de la Instal??laci??**
- Un cop creada la m??quina, feu clic a "Start" per iniciar-la i comen??ar la instal??laci?? del servidor.

![Inici de la instal??laci?? del servidor](https://chaminita94.github.io/mkdocs/custom/aaea.png)

**Selecci?? de la Configuraci?? Inicial**
- A la primera pestanya, seleccioneu l'idioma, el format de l'hora, la moneda i el teclat.
- Feu clic a "Siguiente" (Seg??ent) i despr??s a "Install" per continuar.

![Selecci?? d'idioma i configuraci?? inicial](https://chaminita94.github.io/mkdocs/custom/server1.png)

**Elecci?? de la Versi?? del Sistema Operatiu**
- A la pestanya seg??ent, seleccioneu la versi?? del sistema operatiu que voleu instal??lar.
- Escolliu la versi?? desitjada i feu clic a "Siguiente".
- La versi?? "Standar Evaluation" ??s sense GUI, has de seleccionar la "Experiencia con GUI" que ??s l'opci?? n??mero dos.

![Selecci?? de la versi?? del sistema operatiu](https://chaminita94.github.io/mkdocs/custom/arara.png)

**Tipus d'Instal??laci??**
- Seleccioneu l'opci?? "Personalitzada" per realitzar una instal??laci?? manual.

![Selecci?? de l'opci?? d'instal??laci?? personalitzada](https://chaminita94.github.io/mkdocs/custom/perf.png)

**Selecci?? del Disc d'Instal??laci??**
- Seleccioneu el disc on voleu instal??lar Windows.
- Si disposeu de diversos discs, assegureu-vos de triar el correcte.

![Selecci?? del disc](https://chaminita94.github.io/mkdocs/custom/disc.png)

**Finalitzaci?? del Proc??s**
- Espereu mentre es completa el proc??s d'instal??laci??.

![Pantalla d'espera mentre s'instal??la](https://chaminita94.github.io/mkdocs/custom/waiting.png)

- Un cop s'ha completat la instal??laci?? de Windows Server, el seg??ent pas ??s seguir les instruccions que apareixen a la pantalla. Aix?? inclou configurar el nom d'usuari i ajustar altres opcions per personalitzar el sistema segons les teves necessitats.

![alt text](https://chaminita94.github.io/mkdocs/custom/finished.png)

### IP Fixa al Servidor
??s important configurar una IP fixa al servidor per evitar que canvi?? cada cop que s'enc??n. Aix?? garanteix que:
- Els clients i dispositius de la xarxa sempre puguin trobar el servidor a la mateixa adre??a IP.
- Es puguin configurar serveis com Active Directory, DNS, DHCP, impressi?? en xarxa o compartici?? de fitxers de manera estable i fiable.
- Es pugui fer administraci?? remota, redirecci?? de ports al router o configuraci?? de tallafocs sense problemes.

### Com assignar una IP fixa al servidor (GUI de Windows)

1. **Obrim la configuraci?? de xarxa**
2. Aneu a Configuraci?? > Xarxa i Internet > Ethernet.
3. Cliqueu a "Canviar opcions de l'adaptador".

```
Configuraci?? > Xarxa i Internet > Ethernet
```

![Ethernet](https://chaminita94.github.io/mkdocs/custom/kekeke.png)

1. **Obrim les propietats del nostre adaptador de xarxa**
2. Feu clic dret sobre l'adaptador Ethernet i seleccioneu "Propietats".

![Propietats](https://chaminita94.github.io/mkdocs/custom/propip.png)

1. **Configurem la IP manualment**
2. Seleccionem Protocol d'Internet versi?? 4 (TCP/IPv4) i cliquem a "Propietats".
3. Marquem l'opci?? "Utilitzar la seg??ent adre??a IP" i hi introdu??m:
   - Adre??a IP fixa (ex: 192.168.1.100)
   - M??scara de subxarxa (ex: 255.255.255.0)
   - Porta d'enlla?? predeterminada (ex: 192.168.1.1)
   - DNS preferit i alternatiu (ex: 1.1.1.1 i 8.8.8.8)

```
192.168.1.100
255.255.255.0
192.168.1.1
1.1.1.1
8.8.8.8
```

![IP manual](https://chaminita94.github.io/mkdocs/custom/ipmanual.png)

1. **Comprovem que s'ha aplicat correctament**
2. Obrim la consola CMD i escrivim:

```bash
ipconfig
```

3. Verifiquem que apareix la IP que hem assignat.

![ipconfig](https://chaminita94.github.io/mkdocs/custom/ipcon.png)

### Per qu?? ??s important tenir una IP fixa?
- **Estabilitat de la xarxa:** serveis com DNS, RDP, FTP o compartici?? de fitxers requereixen que l'adre??a IP del servidor sigui constant.
- **Evita errors:** si l'IP canvia, els usuaris podrien perdre la connexi?? al servidor o accedir a un altre dispositiu incorrectament.
- **Configuracions avan??ades:** el redireccionament de ports al router o tallafocs necessita con??ixer l'adre??a IP exacta.

???? Si s'utilitza DHCP, es pot reservar una IP per MAC al servidor DHCP, per?? per servidors ??s millor una IP est??tica manual per seguretat i control.

## Qu?? ??s Windows 10 Pro?
Windows 10 Pro ??s una edici?? del sistema operatiu Windows 10 dissenyada especialment per a professionals i entorns empresarials. Aquesta versi?? incorpora caracter??stiques addicionals en comparaci?? amb l'edici?? Home, com ara:
- **Seguretat avan??ada:** Inclou eines i funcionalitats millorades per a la seguretat, com BitLocker per a xifrar dades i funcions de gesti?? d'identitat.
- **Gesti?? empresarial:** Permet la gesti?? de dispositius i pol??tiques de seguretat a trav??s d'eines com Active Directory i Microsoft Intune.
- **Funcions de productivitat:** Suporta funcions que faciliten la multitasca i l'acc??s a recursos empresarials, millorant la connectivitat i la integraci?? amb xarxes corporatives.

### ??s i Aplicacions
Windows 10 Pro ??s ??mpliament utilitzat en entorns professionals i empresarials. Algunes de les seves aplicacions inclouen:
- Desenvolupament de programari i proves en entorns virtuals.
- Gesti?? d'infraestructures inform??tiques en empreses.
- ??s en entorns on la seguretat de la informaci?? ??s priorit??ria.
- Tasques de productivitat di??ria que requereixen funcions avan??ades i una major compatibilitat amb xarxes corporatives.

[Lic??ncies de windows.](https://chaminita94.github.io/mkdocs/licenciawind/)

### Aspectes Econ??mics
??s important destacar que Windows 10 Pro no ??s un sistema operatiu gratu??t. Per a la seva instal??laci?? i ??s, ??s necessari adquirir una llic??ncia v??lida. Aquesta inversi?? ??s recomanada per a entorns professionals i empresarials, on les funcionalitats addicionals i el suport t??cnic justifiquen el cost.

## Instal??laci?? de Windows 10 PRO
A continuaci??, en el proc??s d'instal??laci?? de Windows 10 Pro en una m??quina virtual mitjan??ant VirtualBox, detallant els passos necessaris per configurar i posar en marxa el sistema operatiu en un entorn virtual.

**Creaci?? de la M??quina Virtual**
- Feu clic a "New" per comen??ar la creaci?? de la m??quina virtual.
- Afegiu el nom a la m??quina virtual.
- Inseriu la ISO de Windows 10 pro.
- Feu clic a "Skip unattended installation" per procedir amb una instal??laci?? manual.

![alt text](https://chaminita94.github.io/mkdocs/custom/w10.png)

**Configuraci?? de Recursos**
- Escolliu la quantitat de RAM i les CPU virtuals o threads que assignareu a la m??quina.
- Deixeu les altres opcions amb els valors per defecte.

![alt text](https://chaminita94.github.io/mkdocs/custom/conf.png)

**Inici de la Instal??laci??**
- Un cop creada la m??quina, feu clic a "Start" per iniciar-la i comen??ar la instal??laci?? de la m??quina.

![alt text](https://chaminita94.github.io/mkdocs/custom/startaa.png)

**Selecci?? de la Configuraci?? Inicial**
- A la primera pestanya, seleccioneu l'idioma, el format de l'hora, la moneda i el teclat.
- Feu clic a "Siguiente" (Seg??ent) i despr??s a "Install" per continuar.

![alt text](https://chaminita94.github.io/mkdocs/custom/lang.png)

**Elecci?? de la Versi?? del Sistema Operatiu**
- A la pestanya seg??ent, seleccioneu la versi?? del sistema operatiu que voleu instal??lar.
- Escolliu la versi?? desitjada i feu clic a "Siguiente".

![alt text](https://chaminita94.github.io/mkdocs/custom/vers.png)

**Tipus d'Instal??laci??**
- Seleccioneu l'opci?? "Personalitzada" per realitzar una instal??laci?? manual.

![alt text](https://chaminita94.github.io/mkdocs/custom/cust.png)

**Selecci?? del Disc d'Instal??laci??**
- Seleccioneu el disc on voleu instal??lar Windows.
- Si disposeu de diversos discs, assegureu-vos de triar el correcte.

![alt text](https://chaminita94.github.io/mkdocs/custom/dd.png)

**Finalitzaci?? del Proc??s**
- Espereu mentre es completa el proc??s d'instal??laci??.

![alt text](https://chaminita94.github.io/mkdocs/custom/araraa.png)

- Un cop s'ha completat la instal??laci?? de Windows 10 Pro, el seg??ent pas ??s seguir les instruccions que apareixen a la pantalla. Aix?? inclou configurar el nom d'usuari i ajustar altres opcions per personalitzar el sistema segons les teves necessitats.

![alt text](https://chaminita94.github.io/mkdocs/custom/donete.png)

## Crear particions en Windows
Per gestionar particions en Windows, utilitzem l'eina Disk Management. Aquesta eina ens permet crear, eliminar i modificar particions dels nostres discs.

![Disk Management](https://chaminita94.github.io/mkdocs/custom/discpart.png)

### Obrir el gestor de discos
Obrim el "Disk Management". Per fer-ho, podem buscar "disk" al men?? d'inici i seleccionar "Create and format hard disk partitions".
Aquesta eina ens mostrar?? els discs disponibles al nostre equip, aix?? com la seva estructura de particions.

![Gestor de discos](https://chaminita94.github.io/mkdocs/custom/diskman.png)

### Redimensionar una partici??
Per redimensionar una partici??, fem clic dret sobre el disc que volem modificar i seleccionem "Shrink Volume".

![Opci?? de reducci??](https://chaminita94.github.io/mkdocs/custom/red.png)

S'obrir?? una finestra que ens permet indicar la quantitat d'espai que volem reduir de la partici?? seleccionada.

![Reduir espai](https://chaminita94.github.io/mkdocs/custom/shrink.png)

Despr??s d'aquesta acci??, veurem un espai no assignat a l'eina de gesti?? de discos.

![Espai no assignat](https://chaminita94.github.io/mkdocs/custom/shrinked.png)

### Crear una nova partici??
Per aprofitar l'espai no assignat, hem de crear una nova partici??. Fem clic dret sobre l'espai no assignat i seleccionem "New Simple Volume".

![Nou volum simple](https://chaminita94.github.io/mkdocs/custom/new.png)

Seguidament, es mostrar?? un assistent on simplement hem de fer Next > Next > Finish.

### Seleccionar el sistema de fitxers
Durant el proc??s, haurem de seleccionar un sistema de fitxers per a la partici??. Els sistemes m??s comuns s??n:
- **NTFS:** Recomanat per a Windows, suporta fitxers grans i permisos avan??ats.
- **FAT32:** Compatible amb molts dispositius, per?? limita la mida dels fitxers a 4 GB.
- **exFAT:** Millor que FAT32 per a dispositius externs, ja que no t?? la limitaci?? de 4 GB per fitxer.

![Opcions de format](https://chaminita94.github.io/mkdocs/custom/next.png)

### Finalitzar el proc??s
Despr??s d'esperar que es completi el formatatge...

![Formatant partici??](https://chaminita94.github.io/mkdocs/custom/waitinga.png)

...la nova partici?? ja estar?? disponible per utilitzar.

![Partici?? creada](https://chaminita94.github.io/mkdocs/custom/donetea.png)

Amb aix??, hem completat la creaci?? d'una partici?? en Windows!

## Punts de Restauraci??
Els punts de restauraci?? serveixen per desfer canvis en el sistema operatiu i recuperar un estat anterior del sistema si alguna cosa va malament (errors de configuraci??, instal??laci?? de programes problem??tics, etc.).
???? ??s una eina molt ??til abans de fer canvis importants en el sistema, com instal??lar drivers o actualitzacions.

### Com crear un punt de restauraci?? manualment
1. Cerquem "Create restore point" al men?? d'inici de Windows.

![Obrir configuraci??](https://chaminita94.github.io/mkdocs/custom/restorep.png)

2. A la pestanya System Protection, seleccionem el disc principal (normalment C:) i fem clic a Configure.

![Protecci?? del sistema](https://chaminita94.github.io/mkdocs/custom/sysp.png)

3. Activem la protecci?? del sistema i definim un percentatge d'espai del disc per a emmagatzemar punts de restauraci??.

![??s de disc](https://chaminita94.github.io/mkdocs/custom/usage.png)

4. Un cop activat, seleccionem el disc i fem clic a Create per generar un nou punt de restauraci??.

![Crear punt](https://chaminita94.github.io/mkdocs/custom/hehe.png)

5. Assignem un nom descriptiu al punt de restauraci?? (per exemple: "Abans d???instal??lar drivers NVIDIA").

![Assignar nom](https://chaminita94.github.io/mkdocs/custom/assnom.png)

6. Esperem que el sistema acabi de crear el punt de restauraci??.

![Creant punt](https://chaminita94.github.io/mkdocs/custom/saving.png)

7. Ja tenim un punt de restauraci?? disponible! Si cal, podem restaurar l???estat del sistema a aquest punt des del mateix men??.

### Restaurar el sistema a un punt anterior
Despr??s de crear un punt de restauraci??, podem provar el seu funcionament:
1. Descarreguem i instal??lem un programa qualsevol per fer la prova.

![Descarregar programa](https://chaminita94.github.io/mkdocs/custom/descar.png)

2. Ara, tornem al men?? de restauraci??: "Create restore point" > System Restore.

![Restaurar sistema](https://chaminita94.github.io/mkdocs/custom/sysr.png)

3. Seleccionem el punt de restauraci?? que hav??em creat pr??viament.
4. Podem fer clic a "Search for affected programs" per veure qu?? s'eliminar?? o modificar??.

![Escaneig de programes afectats](https://chaminita94.github.io/mkdocs/custom/escana.png)

?????? El sistema ens mostra els programes i controladors que es veuran afectats. ???? Els nostres arxius personals NO es perden, nom??s es modifiquen programes i configuracions del sistema.

### Resultat de la restauraci??
Quan finalitza el proc??s, el sistema torna a l???estat en qu?? es trobava en el moment del punt de restauraci??. Aix?? pot eliminar:
- Programes instal??lats despr??s del punt
- Actualitzacions del sistema
- Canvis en el registre de Windows

???? ??s una eina molt ??til per desfer errors sense haver de reinstal??lar tot el sistema.

## Instal??laci?? d'aplicacions
En Windows ??s molt m??s senzill instal??lar aplicacions que en Linux.
Per exemple, si no vols utilitzar el Microsoft Edge, pots descarregar-te el Google Chrome simplement accedint a la [web de Chrome](https://www.google.com/chrome) i descarregant-lo.

![Chrome web](https://chaminita94.github.io/mkdocs/custom/chromea.png)

Fes doble clic en l'arxiu que t'has descarregat i segueix les instruccions que apareixen en pantalla.

![Instal??lador Chrome](https://chaminita94.github.io/mkdocs/custom/ch.png)

I ja ho tindr??em.

![Chrome instal??lat](https://chaminita94.github.io/mkdocs/custom/ch2.png)

### Instal??lar paquets via PowerShell
Tamb?? pots instal??lar paquets utilitzant PowerShell. Obre el PowerShell en mode administrador i escriu la comanda seg??ent per instal??lar CCleaner:

```powershell
winget install --id=Piriform.CCleaner -e
```

![Instal??laci?? de CCleaner amb PowerShell](https://chaminita94.github.io/mkdocs/custom/cclea.png)

Espera uns instants, i ja ho tindr??s instal??lat.

![PowerShell mostrant l'estat de la instal??laci??](https://chaminita94.github.io/mkdocs/custom/power.png)
