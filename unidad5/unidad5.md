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

## Funcionament
El sistema utilitza eines com apt-mirror i apache2 per baixar i servir localment els paquets d'actualitzacions. Quan els clients executen apt update, es connecten a la IP del servidor central per obtenir els paquets, assegurant una gestió centralitzada de les actualitzacions.

Centralització dels paquets: El servidor manté una còpia local de tots els paquets necessaris.
Actualització amb apt update: Els clients descarreguen les actualitzacions des del servidor, evitant connexions directes als repositoris oficials.

## Usos i Beneficis Pràctics
Aquest model de servidor és especialment útil en entorns on:

### Entorns corporatius: Es necessita un control estricte de les versions per garantir la compatibilitat i la seguretat en tots els dispositius.
### Xarxes amb restriccions d'accés a Internet: Permet que els clients actualitzin els seus sistemes sense exposar-los directament a Internet.
### Proves prèvies d'actualitzacions: Es poden validar i aprovar les actualitzacions en un entorn controlat abans de distribuir-les a tots els clients.
### Auditoria i control: El servidor central pot registrar els paquets descarregats i les actualitzacions, facilitant el seguiment i la resolució d'incidències.



