# AUDITORIA I MONITORATGE
## AUDITORIA DE FITXERS I INICI DE SESSIÓ

Obrim la finestra d'Executar prement les tecles `Windows + R` i escrivim `secpol.msc` per obrir la Directiva de seguretat local.

<img width="413" height="206" alt="image" src="https://github.com/user-attachments/assets/b4cbaccb-bc0d-4a45-bc1f-91a50fc26d61" />

A la Directiva de seguretat local, naveguem fins a **Configuración de seguridad > Directivas locales > Directiva de auditoría**. A la part dreta, seleccionem **Auditar eventos de inicio de sesión**.
   
<img width="784" height="337" alt="image" src="https://github.com/user-attachments/assets/4c4841ca-2bd2-4c81-8ad2-32a8a636722d" />

A les propietats d'aquesta directiva, marquem les caselles per auditar els intents de tipus **Correcto** i **Erróneo** i apliquem els canvis.
   
<img width="414" height="502" alt="image" src="https://github.com/user-attachments/assets/8b4f1e72-aafb-4160-8153-019c146f85dd" />

Repetim el mateix procés per a la directiva **Auditar eventos de inicio de sesión de cuenta**, activant-ne l'auditoria tant per a èxits (**Correcto**) com per a errors (**Erróneo**).
<img width="416" height="501" alt="image" src="https://github.com/user-attachments/assets/30427b6b-cc8d-43d3-81e1-55660d9748f7" />

Comprovem al panell que s'han aplicat correctament els canvis a les directives escollides (inici de sessió, inici de sessió de compte, accés a objectes, canvi de directives i administració de comptes).
   
<img width="526" height="216" alt="image" src="https://github.com/user-attachments/assets/3e8ccc5c-402e-47b0-94bf-cd80057fb16a" />

Ens dirigim al disc local `C:\` i localitzem la carpeta on aplicarem l'auditoria de fitxers, que en aquest cas s'anomena `LAB_AUDIT`.
    
<img width="615" height="160" alt="image" src="https://github.com/user-attachments/assets/78a8566d-45cc-4e2f-9fe6-8ea3ffb00f2b" />

A l'interior de la carpeta `LAB_AUDIT`, observem que hi ha dos fitxers de text preparats: `secret.txt` i `test.txt`.
    
<img width="650" height="133" alt="image" src="https://github.com/user-attachments/assets/0120247a-0d37-480e-81bc-54af0846b9f2" />

Accedim a les propietats de la carpeta `LAB_AUDIT`, a la pestanya **Seguridad** i fem clic a **Avanzadas**. A la pestanya **Permisos**, ens assegurem que el grup **Usuarios autentificados** tingui permisos de **Modificar**.
    
<img width="763" height="522" alt="image" src="https://github.com/user-attachments/assets/5e47189d-b4bd-4b27-9911-5686edc8ff22" />

Tanquem la sessió de l'administrador i iniciem sessió al sistema amb les credencials de l'usuari creat prèviament (`usuari1`).
    
<img width="464" height="354" alt="image" src="https://github.com/user-attachments/assets/c9131b44-e6a0-4bf2-9229-a7f2f8ae0439" />

Amb la sessió de l'`usuari1` oberta, editem el fitxer `test.txt` situat dins de `LAB_AUDIT`, hi escrivim algun text (per exemple, "HOLA COM ESTAS?") i el desem per generar un esdeveniment d'escriptura.
    
<img width="433" height="181" alt="image" src="https://github.com/user-attachments/assets/405fcaa0-1825-4f30-9b0c-7bb14781fb60" />

A continuació, fem clic dret sobre el fitxer `secret.txt` i seleccionem **Eliminar** per esborrar-lo, fet que també generarà un esdeveniment auditat al sistema per l'esborrat de l'arxiu.
    
<img width="430" height="365" alt="image" src="https://github.com/user-attachments/assets/42fbe483-582d-4865-9bf0-9b9b2f5e03ed" />

Tornem a iniciar sessió com a administrador i obrim el **Visor de eventos** (Visor d'esdeveniments). Dins de **Registros de Windows > Seguridad**, podem trobar esdeveniments de tipus **Error de auditoría** (com l'Id. 4656), que ens informa d'un intent fallit d'accés o manipulació d'un objecte.
    
<img width="717" height="227" alt="image" src="https://github.com/user-attachments/assets/1ca19bb9-bba5-44c8-adfd-1e36ced63beb" />

També hi observem esdeveniments de tipus **Auditoría correcta** (Id. 4658 i 5158), que ens detallen que certes operacions com el tancament o la manipulació d'objectes (lectura/escriptura de l'arxiu o l'esborrament) s'han realitzat satisfactòriament.
    
<img width="655" height="99" alt="image" src="https://github.com/user-attachments/assets/a0b0827e-bd34-45f5-a790-55b7a08029d6" />

De la mateixa manera, trobem esdeveniments d'**Auditoría correcta** com l'Id. 4690 corresponent a la "Manipulación de identificadores", indicant que l'obertura del gestor (handle) s'ha fet amb èxit.
    
<img width="611" height="19" alt="image" src="https://github.com/user-attachments/assets/415953d3-51ee-4c42-a2ed-604f8a589611" />

## MONITORITZACIÓ DE RENDIMENT

Obrim l'**Administrador de tareas** (Administrador de tasques). A la pestanya **Procesos**, veiem la llista completa de processos en execució, detallant quin ús fa cadascun respecte a la **CPU**, la **Memòria**, el **Disc** i la **Xarxa**.
   
<img width="549" height="332" alt="image" src="https://github.com/user-attachments/assets/c8c24f7c-c04e-4448-9b5b-2dbc6d74286f" />

Anant a la pestanya **Rendimiento** (Rendiment), podem observar els gràfics de consum globals en temps real. Per exemple, veiem el gràfic de consum d'una **CPU** AMD Ryzen 5 2600X, així com l'estat de la memòria, el disc i la xarxa al tauler esquerre.

<img width="1283" height="426" alt="image" src="https://github.com/user-attachments/assets/c9c711fc-b735-45e9-91f5-f291a7d6f6ea" />

A la pestanya **Detalles** (Detalls), se'ns mostra informació més avançada de cada procés en execució, com el seu identificador (**PID**), l'estat, quin **usuari** (SYSTEM, alumne, usuari1, etc.) l'està executant i el consum detallat.

<img width="826" height="327" alt="image" src="https://github.com/user-attachments/assets/7603b560-90db-4ea8-bfb1-bcbbbea31d39" />

Per a una anàlisi més profunda, obrim el **Monitor de recursos**. A la pestanya **Información general** (Informació general), obtenim vistes desglossades amb gràfics simultanis del consum de CPU, disc, xarxa i memòria per diagnosticar ràpidament el rendiment de l'equip.

<img width="1267" height="392" alt="image" src="https://github.com/user-attachments/assets/e8b8c66c-bdda-466f-8714-35bbc9af5903" />

Finalment, a la pestanya **Red** (Xarxa) del Monitor de recursos, podem visualitzar detalladament quins processos estan fent ús d'internet o xarxa local, indicant els enviaments i recepcions (B/s) així com les connexions TCP establertes i els ports d'escolta.

<img width="1270" height="374" alt="image" src="https://github.com/user-attachments/assets/cf06c71c-6e72-4da1-aedc-98d2ff93c71b" />

<img width="1069" height="477" alt="image" src="https://github.com/user-attachments/assets/1000aff7-c8e1-4c1b-bb27-0fd1b3c128c5" />

