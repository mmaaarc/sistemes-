# Introducció a RAID en entorns Windows

Els **RAID (Redundant Array of Independent Disks)** són tècniques per combinar diversos discs físics en una unitat lògica amb l’objectiu de millorar el **rendiment**, la **capacitat** o la **tolerància a fallades**.

A Windows i Windows Server, el RAID es pot implementar de dues maneres principals:

* **RAID per programari**: a través del Gestor de discs (Disk Management) o **Storage Spaces**.
* **RAID per maquinari**: mitjançant una controladora RAID configurada des del BIOS/UEFI o eines del fabricant.

**Tipus de RAID habituals a Windows**

| Nivell RAID | Descripció | Disponibilitat a Windows | Avantatges | Inconvenients |
| --- | --- | --- | --- | --- |
| **RAID 0** | Distribució de dades entre discos (striping), sense redundància | Sí (Gestor de discs) | Alt rendiment, ús total de la capacitat | Cap tolerància a fallades |
| **RAID 1** | Mirall de dades entre dos discos | Sí (Gestor de discs) | Alta fiabilitat, fàcil de configurar | Capacitat efectiva reduïda al 50% |
| **RAID 5** | Striping amb paritat distribuïda | Només amb controladora RAID o Storage Spaces (Windows Server) | Bon equilibri entre capacitat i redundància | Mínim 3 discos; rendiment d’escriptura inferior |
| **RAID 10** | Combinació de RAID 1 i RAID 0 | Només amb controladora RAID | Molt alt rendiment i seguretat | Cost elevat, necessita mínim 4 discos |

> ⚠️ **Nota:** Windows no suporta RAID 6 per programari. Aquest nivell només està disponible mitjançant controladores RAID avançades.

**Storage Spaces (Windows 10/11 i Server)**

**Storage Spaces** és la solució moderna de RAID per programari integrada a Windows i Windows Server.

### Tipus de configuració disponibles:

* **Simple (RAID 0):** Només distribueix dades. No tolera fallades.
* **Mirall doble o triple (RAID 1/1+):** Redundància a 2 o 3 còpies.
* **Paritat:** Similar al RAID 5. Protegeix contra fallada d’1 disc (o 2 amb doble paritat en Windows Server).

### Avantatges de Storage Spaces:

* Reconfiguració en calent (hot swap).
* Alertes i supervisió des del tauler de control.
* Integració amb **ReFS** (Resilient File System) per a entorns crítics.

## Consideracions a l'hora de configurar RAID a Windows

* 🔧 **Uniformitat de discs:** És recomanable utilitzar discos de la mateixa mida, velocitat i tipus.
* 🧱 **Planificació prèvia:** El tipus de RAID escollit determinarà la redundància, rendiment i capacitat útil.
* 🔁 **Còpies de seguretat:** RAID no substitueix una política de còpies de seguretat. Cal tenir backups externs.

## Comparativa: RAID per maquinari vs RAID per programari (Windows)

| Característica | RAID per programari (Windows) | RAID per maquinari |
| --- | --- | --- |
| **Cost** | Sense cost addicional | Pot requerir controladora dedicada |
| **Rendiment** | Menor (usa recursos del sistema) | Major (gestió autònoma) |
| **Configuració** | Fàcil (interfície gràfica) | Més complexa, habitualment via BIOS |
| **Gestió de fallades** | Limitada en alguns nivells | Avançada (alertes, hot spare, etc.) |
| **Compatibilitat** | Vinculat a Windows | Pot ser multiplataforma |

---

## Recursos útils

* [Configuració de Storage Spaces a Windows (Microsoft Docs)](https://learn.microsoft.com/windows-server/storage/storage-spaces/)
* [RAID vs Storage Spaces – Comparativa tècnica (TechNet)](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn387076(v=ws.11))
* [ZFS a Windows (projectes alternatius)](https://openzfs.org)
# Configuració de RAID 5 a Windows (Gestió de discs)

A Windows Server, podem crear un **RAID 5 per programari** utilitzant l’eina de **Gestió de discs**. Aquest tipus de RAID ofereix **redundància mitjançant paritat**, permetent la recuperació de dades en cas de fallada d’un disc.

> ⚠️ **Important:** Aquesta funcionalitat només està disponible a **Windows Server** (no està disponible a Windows 10/11).

## Requisits previs

* Mínim **3 discos físics** no assignats (sense particions i inicialitzats).
* Els discos han d’estar convertits a **dinàmics** per poder formar un volum RAID 5.
* Opcionalment, espai reservat suficient per a dades i paritat.

---

## Passos per crear un RAID 5

**Connectar els discos**

Connecta i verifica que el sistema detecti **3 o més discos nous**. El RAID 5 requereix almenys **2 discos per a dades** i **1 disc per a la paritat**.

![Connexió de discs](../img/img/raidwind.png)

---

**Obrir la Gestió de discs**

Es pot accedir a la Gestió de discs de diverses formes:

* Fent clic dret sobre el botó de **Inici** i seleccionant **"Gestió de discs"**.
* Obrint **Executar (Win + R)** i escrivint `diskmgmt.msc`.

![Accés a la gestió de discs](../img/img/raid12.png)

---

**Inicialitzar els discos nous**

Quan accedeixis a la Gestió de discs, el sistema detectarà els discos nous i et demanarà si vols **inicialitzar-los**. Accepta i selecciona el tipus de partició **GPT** o **MBR**, segons el cas.

![Inicialització de discos](../img/img/3disc.png)

---

**Convertir a discs dinàmics**

Abans de crear el RAID, cal convertir els discos a **dinàmics**:

* Clic dret sobre cada disc nou.
* Selecciona **"Convertir a disc dinàmic"**.
* Aplica els canvis.

---

**Crear el volum RAID 5**

* Clic dret sobre un dels discos amb espai no assignat.
* Selecciona **"Nou volum RAID-5..."**.

![Opció de RAID 5](../img/img/ieas.png)

---

**Assistents i selecció de discos**

S’iniciarà l’assistent per crear el volum RAID 5.

* Fes clic a **Següent**.
* Afegeix els altres discos que formaran part del RAID 5.

![Assistents RAID 5](../img/img/raidas.png)

![Selecció de discos](../img/img/iaas.png)

---

**Assignació de lletra i format**

* Assigna una **lletra de la unitat** (ex. E:).
* Dona un **nom** al volum.
* Selecciona el **sistema de fitxers**:
* **NTFS**: Recomanat per a la majoria de casos.
* **ReFS**: (Resilient File System) útil en entorns de servidor. Ofereix integritat automàtica, detecció d’errors i resistència a corrupcions.

> ℹ️ **Nota:** ReFS no és compatible amb totes les versions ni funcions (per exemple, no permet compressió ni encriptació).

![Assignació de lletra](../img/img/lletra.png)
![Format del volum](../img/img/fata.png)

---

**Confirmació i creació**

Un cop revisades les opcions, Windows mostrarà un avís indicant que els discos seran convertits i es perdran dades si n’hi haguessin.

* Fes clic a **"Sí"** per continuar.

![Confirmació final](../img/img/yes.png)

---

**Finalització**

Després d’uns instants, el volum RAID 5 apareixerà com a format i llest per ser utilitzat.

![RAID 5 creat](../img/img/doneRA.png)

---

## Consideracions finals

* El **RAID 5** proporciona un bon equilibri entre capacitat i seguretat, ja que pot tolerar la fallada d’**un únic disc**.
* El rendiment d’escriptura és lleugerament inferior a RAID 0 o 1, ja que implica càlcul de paritat.
* Es recomana monitoritzar l’estat dels discs i tenir còpies de seguretat addicionals.

---

## Simulació de fallada d’un disc en RAID 5

Una de les funcions principals del **RAID 5** és la seva capacitat de continuar funcionant en cas que un dels discs falli, gràcies al sistema de **paritat distribuïda**. Aquesta simulació mostra com es comporta el sistema davant d'una fallada i com es pot recuperar.

---

### Preparació de dades per a la prova

Primer es creen alguns fitxers dins la unitat RAID 5 per comprovar si es mantenen disponibles durant i després de la fallada.

![Fitxers de prova creats](../img/img/testinga.png)

---

**Simulació de la fallada d’un disc**

Amb un clic dret sobre un dels discs (per exemple, **Disc 2**), aquest es desconnecta per simular una fallada física.

El sistema detecta l'error i mostra un **avís de pèrdua de redundància**, però **les dades continuen sent accessibles** gràcies a la informació de paritat.

![Disc desconnectat](../img/img/deesc.png)

---

**Comprovació del funcionament**

Tot i la fallada, es poden seguir llegint fitxers antics i fins i tot crear-ne de nous dins la mateixa unitat RAID. El sistema continua operatiu.

![Accés i escriptura activa](../img/img/keke.png)

---

**Substitució del disc avariat**

S’afegeix un disc nou al sistema, que substitueix el que ha fallat.

![Nou disc afegit](../img/img/jar.png)

---

### Recuperació del volum RAID

A la Gestió de discs, amb un clic dret sobre un dels discs actius del volum RAID, es selecciona l’opció **"Reactivar RAID"**.

Apareixerà una finestra per seleccionar el nou disc que es vol afegir al volum. En fer-ho, s’inicia el procés de **reconstrucció i sincronització** automàtica de les dades perdudes mitjançant la informació de paritat.

![Reactivació del RAID](../img/img/reparar.png)

---

**Sincronització i restauració completa**

Durant la sincronització, el sistema regenera les dades al disc nou. Un cop finalitzat el procés, el volum RAID torna a estar **en estat òptim**, amb redundància restaurada i totes les dades intactes.

![Sincronització activa](../img/img/sinc.png)

---

**Verificació final**

Es comprova la unitat RAID i es constata que **tots els fitxers originals estan disponibles** i que el sistema ha continuat funcionant sense pèrdua de dades.

![Dades recuperades](../img/img/raid41.png)

---

**Conclusió**

Aquesta simulació demostra com un volum **RAID 5 a Windows Server** és capaç de:

* Detectar automàticament una fallada de disc.
* Mantenir el sistema operatiu i accessible.
* Reconstruir la redundància automàticament després de substituir el disc.
* Protegir les dades sense interrupció del servei.

> 💡 **Recomanació:** Tot i tenir tolerància a fallades, és essencial mantenir còpies de seguretat externes. RAID **no substitueix** un pla de backups.
# Monitoratge

## Monitoratge en Windows

El monitoratge en sistemes Windows és fonamental per assegurar el bon funcionament dels equips, prevenir errors i detectar problemes de rendiment o seguretat. Windows ofereix diverses eines integrades, així com aplicacions de tercers, per a monitorar tant el maquinari com els serveis del sistema, l’ús de recursos, la xarxa, processos i molt més.

### Eines integrades en Windows

Windows disposa de diverses eines pròpies per fer tasques de monitoratge:

#### Monitor de Rendiment (Performance Monitor)

Una eina avançada que permet recollir i analitzar dades del sistema en temps real o de manera programada. Pots afegir comptadors per controlar l'ús de CPU, memòria, disc, xarxa i més.

* **Com obrir-la:** `Win + R` ➝ escriu `perfmon`

![alt text](../img/img/adasdsd.png)

**Utilitats:**

* Crear informes personalitzats.
* Registrar dades durant un període de temps.
* Supervisar serveis específics o processos.

![alt text](../img/img/lelele.png)

I podem visualitzar el processador.

![alt text](../img/img/jejajha.png)

#### Gestor de tasques (Task Manager)

Ofereix una visió ràpida dels recursos utilitzats pel sistema i processos actius.

* **Com obrir-lo:** `Ctrl + Shift + Esc` o clic dret a la barra de tasques ➝ "Gestor de tasques".
* **Pots veure:**
* Ús de CPU, RAM, disc i xarxa.
* Aplicacions en execució i processos en segon pla.
* Serveis i inici d’aplicacions.

![alt text](../img/img/taskm.png)

El rendiment del equip.

![alt text](../img/img/jujr.png)

També pots observar els estats i els detalls dels procéssos a més del seu PID.

![alt text](../img/img/stats.png)

#### Visualitzador d'esdeveniments (Event Viewer)

Permet consultar els esdeveniments del sistema com errors, avisos i informació important.

* **Com obrir-lo:** `Win + R` ➝ escriu `eventvwr`
* **Categories principals:**
* Registres del sistema.
* Registres d’aplicacions.
* Registres de seguretat (auditories, intents d'inici de sessió, etc.).

![alt text](../img/img/eventv.png)

A la finestra que apareix, pots aplicar diversos filtres:

* Rang de dates
* Nivell de l'esdeveniment (Informatiu, Advertència, Error, Crític)
* Registre (p. ex., Sistema, Aplicació, Seguretat)
* **Identificador del procés (PID)**, per exemple `131`

![alt text](../img/img/personal.png)

Quan apliques aquest filtre pel **PID 131**, es mostraran només els esdeveniments relacionats amb aquest procés concret.

![alt text](../img/img/newr.png)
# Auditories

### Crear una auditoria en Windows

L’auditoria en Windows permet registrar accions específiques del sistema i dels usuaris, com l’inici de sessió, l’accés a fitxers o canvis en la configuració. És una eina clau per garantir la seguretat i el compliment normatiu en entorns professionals.

Per activar i configurar una auditoria, cal fer-ho mitjançant **polítiques de seguretat local** o **GPOs (Group Policy Objects)**.

---

#### Activar l’auditoria amb la política de seguretat local

Obre l’eina `secpol.msc` (`Win + R` ➝ escriu `secpol.msc` i prem Enter).

Ves a:  
**Polítiques locals** ➝ **Política d’auditoria**

![alt text](../img/img/auditr.png)

* Aquí pots activar les categories d’auditoria, com ara:
* **Esdeveniments d'inici i tancament de sessió**
* **Accés a objectes**
* **Canvis de política**
* **Esdeveniments del sistema**
* Fes doble clic sobre la política que vols activar i marca:
* **Èxit** (quan l’acció es fa correctament)
* **Error** (quan l’acció falla)

![alt text](../img/img/ikar.png)

Obre el **Visualitzador d'esdeveniments** (`eventvwr`)

* Fixa’t en els identificadors d'esdeveniments, com per exemple:
* **4624**: Inici de sessió correcte
* **4625**: Inici de sessió fallit

![alt text](../img/img/erorrl.png)

---

#### Exemple: Auditar l'accés a un fitxer o carpeta

**Activa l’auditoria d'accés a objectes** a `secpol.msc` com s'ha explicat anteriorment.

Clic dret a la carpeta o fitxer que vols auditar ➝ **Propietats** ➝ Pestanya **Seguretat**

Fes clic a **Avançat** ➝ Pestanya **Auditoria**

* Afegeix un usuari o grup (o “Tots”) i defineix els permisos a auditar, per exemple:
* **Lectura**
* **Escriptura**
* **Eliminar**

![alt text](../img/img/jurt.png)

Ara, cada acció d'accés quedarà registrada al **Visualitzador d’esdeveniments**, dins del registre **Seguretat** (`eventvwr.msc`).

![alt text](../img/img/iraras.png)

Per veure els resultats: Obre el **Visualitzador d'esdeveniments** (`eventvwr`)

Fixa’t en els identificadors d'esdeveniments, com per exemple:

* **4624**: Inici de sessió correcte
* **4625**: Inici de sessió fallit
* **4663**: Accés a un objecte (fitxer, carpeta)
* **4688**: Creació d’un procés

---

## Configurar una GPO per auditar els inicis de sessió (login)

En un entorn de domini amb Active Directory, pots configurar una **GPO (Group Policy Object)** per registrar els intents d'inici i tancament de sessió dels usuaris. Aquesta informació és essencial per a la seguretat i l’auditoria dels accessos als sistemes.

### Obrir la consola de gestió de polítiques de grup

* Al controlador de domini, obre la consola **"Group Policy Management"** (`gpmc.msc`).
* Fes clic dret sobre l’OU (Organizational Unit) o el domini on vols aplicar la GPO.
* Selecciona **"Create a GPO in this domain, and Link it here..."**
* Dona-li un nom (ex: `Auditoria-IniciSessio`) i prem **OK**.

---

**Editar la GPO**

Ves a:

Configuració de l'equip ➝ Configuració de Windows ➝

Configuració de seguretat ➝ Polítiques locals ➝ Política d’auditoria

![alt text](../img/img/iara.png)

**Fes doble clic a la política:**

Audit logon events (Auditar els esdeveniments d’inici de sessió)

Marca les opcions:

* **Success (Èxit)**
* **Failure (Error)**

![alt text](../img/img/audgp.png)

--

### Exemple pràctic: Monitoratge d'autenticacions i accessos a directoris

Amb el **Visualitzador d'esdeveniments**, podem monitorar tant els intents d'autenticació d'usuaris (per exemple, si introdueixen una contrasenya incorrecta) com els accessos a directoris compartits via GPO.

---

**Autenticació Kerberos (esdeveniment ID 4771)**

Quan filtrem el Visualitzador d'esdeveniments pel **ID 4771**, podem detectar errors d'autenticació amb Kerberos. A la següent imatge, observem com l’usuari `Jorge` ha introduït una contrasenya incorrecta diverses vegades:

![alt text](../img/img/kerb.png)

Aquest tipus d'esdeveniment indica que el servei Kerberos ha rebut una sol·licitud de tiquet (TGT), però no ha pogut verificar la contrasenya.

---

**Autenticació correcta (esdeveniment ID 4776)**

Quan un usuari introdueix correctament les seves credencials, es genera un esdeveniment amb **ID 4776**. Això indica que l'autenticació NTLM ha estat satisfactòria:

![alt text](../img/img/correc.png)

Aquesta informació és útil per comprovar l’èxit dels intents d’accés després d’errors previs.

---

**Accés a un directori compartit via GPO**

Per monitorar l'accés a directoris compartits, primer hem d’haver configurat prèviament l’auditoria d’accés a objectes mitjançant una **GPO** (vegeu secció anterior). Un cop aplicada, podem realitzar proves pràctiques.

Per exemple, iniciem sessió amb l’usuari `Jorge` i:

* Accedim al directori compartit.
* Creem o modifiquem un fitxer.

![alt text](../img/img/ura.png)

---

**Comprovació de l’accés al directori**

Si l’auditoria està activa, aquests accessos quedaran registrats al Visualitzador d'esdeveniments com a esdeveniments amb **ID 4663**, que indiquen accés a un objecte (fitxer o carpeta):

![alt text](../img/img/comar.png)

Aquest esdeveniment detalla:

* El fitxer o carpeta accedit.
* L’usuari que ha fet l’acció (`Jorge` en aquest cas).
* El tipus d’acció (lectura, escriptura, etc.).

---


# Configuració de RAID 5 a Windows (Gestió de discs)

A Windows Server, podem crear un **RAID 5 per programari** utilitzant l’eina de **Gestió de discs**. Aquest tipus de RAID ofereix **redundància mitjançant paritat**, permetent la recuperació de dades en cas de fallada d’un disc.

> ⚠️ **Important:** Aquesta funcionalitat només està disponible a **Windows Server** (no està disponible a Windows 10/11).

## Requisits previs

* Mínim **3 discos físics** no assignats (sense particions i inicialitzats).
* Els discos han d’estar convertits a **dinàmics** per poder formar un volum RAID 5.
* Opcionalment, espai reservat suficient per a dades i paritat.

---

## Passos per crear un RAID 5

**Connectar els discos**

Connecta i verifica que el sistema detecti **3 o més discos nous**. El RAID 5 requereix almenys **2 discos per a dades** i **1 disc per a la paritat**.

![Connexió de discs](../custom/raidwind.png)

---

**Obrir la Gestió de discs**

Es pot accedir a la Gestió de discs de diverses formes:

* Fent clic dret sobre el botó de **Inici** i seleccionant **"Gestió de discs"**.
* Obrint **Executar (Win + R)** i escrivint `diskmgmt.msc`.

![Accés a la gestió de discs](../custom/raid12.png)

---

**Inicialitzar els discos nous**

Quan accedeixis a la Gestió de discs, el sistema detectarà els discos nous i et demanarà si vols **inicialitzar-los**. Accepta i selecciona el tipus de partició **GPT** o **MBR**, segons el cas.

![Inicialització de discos](../custom/3disc.png)

---

**Convertir a discs dinàmics**

Abans de crear el RAID, cal convertir els discos a **dinàmics**:

* Clic dret sobre cada disc nou.
* Selecciona **"Convertir a disc dinàmic"**.
* Aplica els canvis.

---

**Crear el volum RAID 5**

* Clic dret sobre un dels discos amb espai no assignat.
* Selecciona **"Nou volum RAID-5..."**.

![Opció de RAID 5](../custom/ieas.png)

---

**Assistents i selecció de discos**

S’iniciarà l’assistent per crear el volum RAID 5.

* Fes clic a **Següent**.
* Afegeix els altres discos que formaran part del RAID 5.

![Assistents RAID 5](../custom/raidas.png)

![Selecció de discos](../custom/iaas.png)

---

**Assignació de lletra i format**

* Assigna una **lletra de la unitat** (ex. E:).
* Dona un **nom** al volum.
* Selecciona el **sistema de fitxers**:
* **NTFS**: Recomanat per a la majoria de casos.
* **ReFS**: (Resilient File System) útil en entorns de servidor. Ofereix integritat automàtica, detecció d’errors i resistència a corrupcions.

> ℹ️ **Nota:** ReFS no és compatible amb totes les versions ni funcions (per exemple, no permet compressió ni encriptació).

![Assignació de lletra](../custom/lletra.png)
![Format del volum](../custom/fata.png)

---

**Confirmació i creació**

Un cop revisades les opcions, Windows mostrarà un avís indicant que els discos seran convertits i es perdran dades si n’hi haguessin.

* Fes clic a **"Sí"** per continuar.

![Confirmació final](../custom/yes.png)

---

**Finalització**

Després d’uns instants, el volum RAID 5 apareixerà com a format i llest per ser utilitzat.

![RAID 5 creat](../custom/doneRA.png)

---

## Consideracions finals

* El **RAID 5** proporciona un bon equilibri entre capacitat i seguretat, ja que pot tolerar la fallada d’**un únic disc**.
* El rendiment d’escriptura és lleugerament inferior a RAID 0 o 1, ja que implica càlcul de paritat.
* Es recomana monitoritzar l’estat dels discs i tenir còpies de seguretat addicionals.

---

## Simulació de fallada d’un disc en RAID 5

Una de les funcions principals del **RAID 5** és la seva capacitat de continuar funcionant en cas que un dels discs falli, gràcies al sistema de **paritat distribuïda**. Aquesta simulació mostra com es comporta el sistema davant d'una fallada i com es pot recuperar.

---

### Preparació de dades per a la prova

Primer es creen alguns fitxers dins la unitat RAID 5 per comprovar si es mantenen disponibles durant i després de la fallada.

![Fitxers de prova creats](../custom/testinga.png)

---

**Simulació de la fallada d’un disc**

Amb un clic dret sobre un dels discs (per exemple, **Disc 2**), aquest es desconnecta per simular una fallada física.

El sistema detecta l'error i mostra un **avís de pèrdua de redundància**, però **les dades continuen sent accessibles** gràcies a la informació de paritat.

![Disc desconnectat](../custom/deesc.png)

---

**Comprovació del funcionament**

Tot i la fallada, es poden seguir llegint fitxers antics i fins i tot crear-ne de nous dins la mateixa unitat RAID. El sistema continua operatiu.

![Accés i escriptura activa](../custom/keke.png)

---

**Substitució del disc avariat**

S’afegeix un disc nou al sistema, que substitueix el que ha fallat.

![Nou disc afegit](../custom/jar.png)

---

### Recuperació del volum RAID

A la Gestió de discs, amb un clic dret sobre un dels discs actius del volum RAID, es selecciona l’opció **"Reactivar RAID"**.

Apareixerà una finestra per seleccionar el nou disc que es vol afegir al volum. En fer-ho, s’inicia el procés de **reconstrucció i sincronització** automàtica de les dades perdudes mitjançant la informació de paritat.

![Reactivació del RAID](../custom/reparar.png)

---

**Sincronització i restauració completa**

Durant la sincronització, el sistema regenera les dades al disc nou. Un cop finalitzat el procés, el volum RAID torna a estar **en estat òptim**, amb redundància restaurada i totes les dades intactes.

![Sincronització activa](../custom/sinc.png)

---

**Verificació final**

Es comprova la unitat RAID i es constata que **tots els fitxers originals estan disponibles** i que el sistema ha continuat funcionant sense pèrdua de dades.

![Dades recuperades](../custom/raid41.png)

---

**Conclusió**

Aquesta simulació demostra com un volum **RAID 5 a Windows Server** és capaç de:

* Detectar automàticament una fallada de disc.
* Mantenir el sistema operatiu i accessible.
* Reconstruir la redundància automàticament després de substituir el disc.
* Protegir les dades sense interrupció del servei.

> 💡 **Recomanació:** Tot i tenir tolerància a fallades, és essencial mantenir còpies de seguretat externes. RAID **no substitueix** un pla de backups.
