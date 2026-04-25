# Sprint1Windows

Windows Server és un sistema operatiu desenvolupat per Microsoft dissenyat per a la gestió de servidors. A diferència de les versions d'escriptori de Windows, està optimitzat per oferir serveis de xarxa, allotjament de bases de dades, administració d'usuaris, gestió de dominis, i altres funcions crítiques per a entorns empresarials i corporatius.

[Licències de windows.](https://chaminita94.github.io/mkdocs/licenciawind/)

### Per a què s'utilitza?
Windows Server s'utilitza en empreses i entorns professionals per proporcionar serveis com:
- Control de dominis amb Active Directory
- Servidor de fitxers i impressió
- Serveis web (IIS)
- Virtualització amb Hyper-V
- Allotjament de bases de dades
- Administració de xarxes i seguretat

### Cost i llicència
Windows Server no és un sistema operatiu gratuït. Microsoft ofereix diferents edicions amb llicències de pagament segons les necessitats de l'empresa. Existeixen edicions com Standard, Datacenter i Essentials, cadascuna amb característiques i preus diferents. No obstant això, es pot obtenir una versió de prova limitada en temps per a proves i aprenentatge.

## Instal·lació de Windows Server en VirtualBox
Aquest apartat explica els passos per instal·lar Windows Server en una màquina virtual amb VirtualBox.

**Creació de la Màquina Virtual**
- Feu clic a "New" per començar la creació de la màquina virtual.
- Afegiu el nom a la màquina virtual.
- Inseriu la ISO de Windows Server.
- Feu clic a "Skip unattended installation" per procedir with una instal·lació manual.

![Captura de la pantalla de creació de la màquina](https://chaminita94.github.io/mkdocs/custom/serviso.png)

**Configuració de Recursos**
- Escolliu la quantitat de RAM i les CPU virtuals o threads que assignareu a la màquina.
- Deixeu les altres opcions amb els valors per defecte.

![Configuració de la RAM i CPU](https://chaminita94.github.io/mkdocs/custom/RAM.png)

**Inici de la Instal·lació**
- Un cop creada la màquina, feu clic a "Start" per iniciar-la i començar la instal·lació del servidor.

![Inici de la instal·lació del servidor](https://chaminita94.github.io/mkdocs/custom/aaea.png)

**Selecció de la Configuració Inicial**
- A la primera pestanya, seleccioneu l'idioma, el format de l'hora, la moneda i el teclat.
- Feu clic a "Siguiente" (Següent) i després a "Install" per continuar.

![Selecció d'idioma i configuració inicial](https://chaminita94.github.io/mkdocs/custom/server1.png)

**Elecció de la Versió del Sistema Operatiu**
- A la pestanya següent, seleccioneu la versió del sistema operatiu que voleu instal·lar.
- Escolliu la versió desitjada i feu clic a "Siguiente".
- La versió "Standar Evaluation" és sense GUI, has de seleccionar la "Experiencia con GUI" que és l'opció número dos.

![Selecció de la versió del sistema operatiu](https://chaminita94.github.io/mkdocs/custom/arara.png)

**Tipus d'Instal·lació**
- Seleccioneu l'opció "Personalitzada" per realitzar una instal·lació manual.

![Selecció de l'opció d'instal·lació personalitzada](https://chaminita94.github.io/mkdocs/custom/perf.png)

**Selecció del Disc d'Instal·lació**
- Seleccioneu el disc on voleu instal·lar Windows.
- Si disposeu de diversos discs, assegureu-vos de triar el correcte.

![Selecció del disc](https://chaminita94.github.io/mkdocs/custom/disc.png)

**Finalització del Procés**
- Espereu mentre es completa el procés d'instal·lació.

![Pantalla d'espera mentre s'instal·la](https://chaminita94.github.io/mkdocs/custom/waiting.png)

- Un cop s'ha completat la instal·lació de Windows Server, el següent pas és seguir les instruccions que apareixen a la pantalla. Això inclou configurar el nom d'usuari i ajustar altres opcions per personalitzar el sistema segons les teves necessitats.

![alt text](https://chaminita94.github.io/mkdocs/custom/finished.png)

### IP Fixa al Servidor
És important configurar una IP fixa al servidor per evitar que canviï cada cop que s'encén. Això garanteix que:
- Els clients i dispositius de la xarxa sempre puguin trobar el servidor a la mateixa adreça IP.
- Es puguin configurar serveis com Active Directory, DNS, DHCP, impressió en xarxa o compartició de fitxers de manera estable i fiable.
- Es pugui fer administració remota, redirecció de ports al router o configuració de tallafocs sense problemes.

### Com assignar una IP fixa al servidor (GUI de Windows)

1. **Obrim la configuració de xarxa**
2. Aneu a Configuració > Xarxa i Internet > Ethernet.
3. Cliqueu a "Canviar opcions de l'adaptador".

```
Configuració > Xarxa i Internet > Ethernet
```

![Ethernet](https://chaminita94.github.io/mkdocs/custom/kekeke.png)

1. **Obrim les propietats del nostre adaptador de xarxa**
2. Feu clic dret sobre l'adaptador Ethernet i seleccioneu "Propietats".

![Propietats](https://chaminita94.github.io/mkdocs/custom/propip.png)

1. **Configurem la IP manualment**
2. Seleccionem Protocol d'Internet versió 4 (TCP/IPv4) i cliquem a "Propietats".
3. Marquem l'opció "Utilitzar la següent adreça IP" i hi introduïm:
   - Adreça IP fixa (ex: 192.168.1.100)
   - Màscara de subxarxa (ex: 255.255.255.0)
   - Porta d'enllaç predeterminada (ex: 192.168.1.1)
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

### Per què és important tenir una IP fixa?
- **Estabilitat de la xarxa:** serveis com DNS, RDP, FTP o compartició de fitxers requereixen que l'adreça IP del servidor sigui constant.
- **Evita errors:** si l'IP canvia, els usuaris podrien perdre la connexió al servidor o accedir a un altre dispositiu incorrectament.
- **Configuracions avançades:** el redireccionament de ports al router o tallafocs necessita conèixer l'adreça IP exacta.

💡 Si s'utilitza DHCP, es pot reservar una IP per MAC al servidor DHCP, però per servidors és millor una IP estàtica manual per seguretat i control.
