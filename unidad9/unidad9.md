# Unidad 9: Auditories i Monitoratge a Windows

En aquesta pràctica configurarem les directives d'auditoria de Windows per fer un seguiment dels inicis de sessió i l'accés als recursos de xarxa, així com la monitorització del rendiment.

## Configuració de Directives d'Auditoria

Per començar, hem d'accedir a les **Directives de Seguretat Local** per configurar quins esdeveniments volem registrar al sistema.

![Accés a Directives de Seguretat Local](../img/u9_image.png)

Dins d'aquest menú, despleguem l'opció de **Directives locals**. Aquesta secció conté les regles bàsiques de seguretat del sistema.

![Directives locals](../img/u9_image-1.png)

A continuació, anem a la **Directiva d'auditoria**, on podrem definir què volem auditar (inicis de sessió, canvis de privilegis, etc.).

![Directiva d'auditoria](../img/u9_image-3.png)

Es recomana utilitzar la **Configuració avançada de la política d'auditoria** per a entorns de servidor, ja que permet un control més precís sobre els esdeveniments registrats.

![Configuració avançada de polítiques](../img/u9_image-8.png)

Habilitem l'auditoria per a diferents esdeveniments com els **inicis de sessió** i els **inicis de sessió de compte**. Això registrarà quan els usuaris entren al sistema.

![Auditoria d'inicis de sessió](../img/u9_image-4.png)
![Auditoria d'inicis de sessió de compte](../img/u9_image-5.png)
![Selecció de qualsevol inici](../img/u9_image-6.png)

També activem altres directives importants, com l'auditoria d'accés a objectes, el seguiment de processos i l'administració de comptes, assegurant-nos que es registrin tant els èxits com les fallades.

![Auditoria de seguiment de processos i objectes](../img/u9_image-7.png)

## Preparació de l'Entorn

Per comprovar que les auditories funcionen correctament, preparem un entorn amb un usuari de proves. En aquest cas, utilitzarem l'usuari **alumne**.

![Creació i configuració de l'usuari alumne](../img/u9_image-09.png)
![Propietats de l'usuari](../img/u9_image-10.png)

Ens assegurem que l'usuari pertany al grup adequat perquè les directives del domini se li apliquin correctament.

![Inici de sessió amb l'usuari alumne](../img/u9_image-11.png)

L'usuari executa comandes bàsiques, com obrir la consola de comandes (`cmd.exe`), per generar esdeveniments de seguiment de processos.

![Obertura de CMD](../img/u9_image-12.png)

A continuació, l'usuari accedeix a un recurs compartit de xarxa per provocar un esdeveniment d'accés a objectes auditat. Utilitzem la comanda `explorer.exe` cap a la ruta UNC del servidor.

![Accés al recurs compartit](../img/u9_image-13.png)
![Explorador obert al recurs](../img/u9_image-14.png)

## Comprovació d'Esdeveniments

Després de realitzar aquestes accions, tornem al servidor i obrim el **Visor d'esdeveniments** (`eventvwr.msc`).

![Obertura del Visor d'esdeveniments](../img/u9_image-15.png)

Dins de **Registres de Windows > Seguretat**, apliquem filtres per cercar els identificadors (IDs) específics que estem auditant, com el 4624 (inici de sessió exitós) o 4625 (inici fallit).

![Registres de Windows](../img/u9_image-16.png)

Podem veure els registres generats per l'accés de l'usuari alumne al recurs compartit i l'obertura de processos. Aquests registres inclouen els intents correctes i els accessos als objectes configurats.

![Inici de sessió registrat](../img/u9_image-17.png)
![Detalls de l'inici de sessió de compte](../img/u9_image-18.png)

## Monitorització i Rendiment

Finalment, analitzem el rendiment del sistema i l'ús de recursos mitjançant les eines de monitorització de Windows.

![Inici del Monitor de Recursos](../img/u9_M-image.png)

Amb el **Monitor de Rendiment** i el **Gestor de Tasques**, observem la càrrega de la CPU i els processos actius per assegurar-nos que no hi ha colls d'ampolla.

![Monitorització de CPU](../img/u9_M-image-1.png)
![Gràfiques de rendiment](../img/u9_M-image-3.png)
![Ús de memòria](../img/u9_M-image-2.png)

Monitoritzem també el rendiment del disc i de la xarxa, revisant la quantitat de dades llegides i escrites per detectar activitats inusuals.

![Monitorització de disc](../img/u9_M-image-4.png)
![Rendiment de xarxa](../img/u9_M-image-5.png)
![Anàlisi detallat de processos](../img/u9_M-image-6.png)
![Estat de la memòria RAM](../img/u9_M-image-7.png)

Podem configurar alertes o conjunts de recopiladors de dades per registrar el rendiment durant períodes prolongats de temps.

![Configuració de recopiladors](../img/u9_M-image-8.png)
![Informes de rendiment generats](../img/u9_M-image-9.png)

Amb això donem per finalitzada la configuració d'auditories i la monitorització de recursos al servidor.
