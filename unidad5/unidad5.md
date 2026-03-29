Monitoratge
Monitoratge i Logs
Els logs són registres que documenten totes les activitats i esdeveniments que ocorren en un sistema. Aquests fitxers recullen informació sobre el funcionament, errors, avisos i altres esdeveniments importants, i serveixen per:

Diagnosticar problemes i errors del sistema.
Monitoritzar el rendiment i el comportament dels serveis.
Auditar activitats per detectar accessos no autoritzats o anomalies de seguretat.
Ajudar en el desenvolupament i la depuració d'aplicacions.

Rotació i Gestió dels Logs
La major part dels logs es guarden a la carpeta /var/log, on cada servei o aplicació té el seu propi fitxer de registre. Aquests fitxers són essencials per monitoritzar el funcionament del sistema, detectar errors, auditar esdeveniments i identificar possibles amenaces de seguretat. A més, els logs segueixen una política de rotació predefinida, la qual permet conservar un historial dels logs antics sense que els fitxers es facin massa grans.

<img width="693" height="406" alt="image" src="https://github.com/user-attachments/assets/7f0ef889-8b07-461b-9c56-e811822e5efa" />


La rotació dels logs es pot programar o configurar editant el fitxer que conté les regles globals per a la gestió i rotació dels logs.


<img width="717" height="626" alt="image" src="https://github.com/user-attachments/assets/9723175c-978f-4a2f-961e-92f5a2842346" />

Si volem configurar una rotació específica per a algun log en concret, hem d'accedir al directori on es poden definir regles personalitzades per als diferents serveis o aplicacions.

<img width="815" height="137" alt="image" src="https://github.com/user-attachments/assets/aa41d489-57f0-46d7-b852-6fcbf4e78f4f" />

Per exemple, la configuració d'Apache2 està programada perquè els seus logs es rotin cada 14 dies.

<img width="867" height="475" alt="image" src="https://github.com/user-attachments/assets/dbad7aef-4b24-4d26-826f-d678680050a1" />

Analització de logs
Els logs es poden analitzar mitjançant eines bàsiques com cat seguit de la ruta del log, però una eina molt més potent és journalctl. Aquesta eina permet consultar els esdeveniments del sistema amb filtres específics, com ara el rang de dates, utilitzant els paràmetres --since i --until. Així, es poden visualitzar només els esdeveniments que t'interessen en un període determinat. Per exemple:

<img width="961" height="353" alt="image" src="https://github.com/user-attachments/assets/693cc6fc-d8eb-4bb8-a9c5-9b55f86ca958" />

Per veure els registres associats a un dispositiu, com un disc, es pot executar:

<img width="938" height="320" alt="image" src="https://github.com/user-attachments/assets/dca80334-c810-4945-9e55-61fbbfba2a32" />

Un altre exemple pràctic és quan aturem un servei, com el de apache, i volem analitzar els seus registres per identificar errors.

<img width="905" height="476" alt="image" src="https://github.com/user-attachments/assets/73b62c15-f985-4366-b299-4ad84b689373" />

Normalment proporciona més informació que systemctl i facilita la recerca d'errors.

<img width="932" height="707" alt="image" src="https://github.com/user-attachments/assets/0757229c-b7ee-45a2-a589-bccd30479b30" />

Logs personalitzats
Amb logs personalitzats, podem modificar el comportament i les alertes dels logs del sistema segons les nostres necessitats. Això inclou canviar la configuració per defecte, definir com es gestionen els diferents tipus de logs i fins i tot enviar-los a un servidor centralitzat mitjançant eines com Samba o SCP. Tot i que configurar-ho manualment pot ser complex, una opció moderna és integrar-ho amb Grafana per visualitzar i analitzar la informació de manera centralitzada.

Per exemple, per modificar la configuració dels logs, pots editar el fitxer de configuració del rsyslog:


Així pots canviar la destinació dels logs, els filtres o les alertes assignades a cadascun.

<img width="910" height="679" alt="image" src="https://github.com/user-attachments/assets/34bad234-f53b-45ca-a745-6380e99e6e25" />



## Servidor d'Actualitzacions
¿Què és un Servidor d'Actualitzacions?
El Servidor d'Actualitzacions és un servidor central que concentra tots els paquets d'actualització. Tots els clients es configuren per apuntar a aquest servidor per descarregar les actualitzacions, evitant així la necessitat d'accedir als repositoris web per defecte.

## Funcionament ##
El sistema utilitza eines com apt-mirror i apache2 per baixar i servir localment els paquets d'actualitzacions. Quan els clients executen apt update, es connecten a la IP del servidor central per obtenir els paquets, assegurant una gestió centralitzada de les actualitzacions.

Centralització dels paquets: El servidor manté una còpia local de tots els paquets necessaris.
Actualització amb apt update: Els clients descarreguen les actualitzacions des del servidor, evitant connexions directes als repositoris oficials.

## Usos i Beneficis Pràctics ##
Aquest model de servidor és especialment útil en entorns on:

### Entorns corporatius:  Es necessita un control estricte de les versions per garantir la compatibilitat i la seguretat en tots els dispositius.
### Xarxes amb restriccions d'accés a Internet:  Permet que els clients actualitzin els seus sistemes sense exposar-los directament a Internet.
### Proves prèvies d'actualitzacions:  Es poden validar i aprovar les actualitzacions en un entorn controlat abans de distribuir-les a tots els clients.
### Auditoria i control:  El servidor central pot registrar els paquets descarregats i les actualitzacions, facilitant el seguiment i la resolució d'incidències.


## Configuració del Servidor
Primerament, s'executa sudo apt update al servidor per actualitzar la llista de paquets. A continuació, s'instal·la el servidor web Apache2 amb la comanda sudo apt install apache2.

<img width="1023" height="447" alt="image" src="https://github.com/user-attachments/assets/7138aa00-d844-4919-ab6c-8f98849989fe" />

Instal·lem el paquet apt-mirror, una eina que permet descarregar una còpia local dels repositoris APT. Aquest paquet s'encarrega de descarregar i sincronitzar els paquets indicats en el fitxer de configuració, de manera que els clients es podran actualitzar des del servidor local en lloc d'accedir directament a Internet.

<img width="1073" height="312" alt="image" src="https://github.com/user-attachments/assets/0059ee92-ea87-4180-8fd8-9d55c6a55d08" />


Editem el fitxer /etc/apt/mirror.list. En aquest fitxer, es comenten les línies que es troben dins de l'apartat (1) i s'afegeix la línia número (2) per definir el repositori o paquet que es vol mirrorar.**

<img width="1028" height="569" alt="image" src="https://github.com/user-attachments/assets/09e8068b-1e6c-4385-a724-d01046bfba52" />

Després, s'executa apt-mirror amb permisos d'administrador (utilitzant sudo) per baixar els paquets definits en el fitxer mirror.list. Aquest procés descarrega els paquets especificats.

<img width="994" height="619" alt="image" src="https://github.com/user-attachments/assets/36600a44-0eb7-4891-8eec-b2edc72ddee1" />

Finalment, s'afegeix un enllaç simbòlic del paquet (per exemple, el paquet de Google) dins del directori /var/www/html, de manera que el contingut descarregat sigui accessible a través d'Apache2.

<img width="921" height="47" alt="image" src="https://github.com/user-attachments/assets/dffcd420-8a46-4a93-aa1f-e3e9039009ce" />

Amb aquests passos, la configuració del servidor queda completa. L'exemple utilitza Google com a referència, però es pot substituir pel repositori o paquet que es desitgi.

Configuració dels Clients
Primer de tot, s'executa sudo apt update per actualitzar la llista de paquets.

A continuació, s'executa la comanda wget -q -O https://dl.google.com/linux/linux_signing_key.pub | apt-key add -  que descarrega la clau de signatura pública des de Google de manera silenciosa i la passa a apt-key per afegir-la al sistema. Això permet verificar l'autenticitat dels paquets que es descarregaran del repositori.

És possible que surti un warning, no pateixis.

<img width="1055" height="93" alt="image" src="https://github.com/user-attachments/assets/724d06a4-ffe3-41d6-b66b-04d88b84224d" />


Després, s'obre el fitxer de configuració de les fonts amb i s'afegeix la ruta del nostre servidor, per exemple:

<img width="719" height="51" alt="image" src="https://github.com/user-attachments/assets/85f96673-661b-44d2-bef2-07413f960fda" />

Un cop guardat el fitxer, s'executa un altre apt update i es pot observar que el paquet es descarrega directament des del servidor amb IP 10.0.2.15.

<img width="805" height="155" alt="image" src="https://github.com/user-attachments/assets/7357588b-8760-4c11-b7c2-888537117614" />

Finalment, s'instal·la el paquet amb
<img width="1168" height="284" alt="image" src="https://github.com/user-attachments/assets/e5302d61-f1bd-4ef2-8561-70f087745ef0" />



