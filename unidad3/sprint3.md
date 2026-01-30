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

## Afegir fitxers 

Un cop creat els fitxers tindre que afegirlos al servidor ldap mitjançant la comanda ldapadd.

<img width="810" height="101" alt="image" src="https://github.com/user-attachments/assets/60b01fc9-5657-403f-bd31-1bf26619f663" />

<img width="809" height="78" alt="image" src="https://github.com/user-attachments/assets/e548b836-2014-44e5-beff-2b8df98b0985" />

<img width="809" height="78" alt="image" src="https://github.com/user-attachments/assets/3d0fc4fe-d270-46aa-9e61-9ae83b949640" />

I ara amb slapcat puc comprovar els objectes creats.

Unitat organitzativa.

<img width="514" height="209" alt="image" src="https://github.com/user-attachments/assets/5500de3e-84db-4c45-8c89-fa721398d8b2" />

Grup.

<img width="501" height="256" alt="image" src="https://github.com/user-attachments/assets/de0dd4e3-1442-4f9f-bd48-e3b7e5a11a10" />

Usuari.

<img width="506" height="495" alt="image" src="https://github.com/user-attachments/assets/14a7f2dc-237c-489b-8808-1bc5ef610a3e" />

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

## Gestió LDAP 

## LDAP SEARCH 

Amb el search podem cercar objectes del servidor ldap.
En aquest exemple faig un search al domini marc.com del usuari alu1 i ens el mostra.

<img width="794" height="652" alt="image" src="https://github.com/user-attachments/assets/bb8d68d4-7d5a-440a-9e29-7e6be710b436" />

Amb aquest ldapsearch puc veure els objectes creats al ldap marc.com

<img width="795" height="53" alt="image" src="https://github.com/user-attachments/assets/addfd714-1088-4b34-8d68-11f46be6d1cc" />

## Comprovació de les Unitats Organitzatives (UOs)

També podem fer una cerca per trobar totes les Unitats Organitzatives (UOs) del domini.

<img width="984" height="106" alt="image" src="https://github.com/user-attachments/assets/3cc34d37-32ea-49a7-b632-3ef7ba1de9d7" />

## ldapmodify

A continuació modifico la password de l'usuari alu1 per tant primer creo el fitxer modify.ldif.

<img width="571" height="29" alt="image" src="https://github.com/user-attachments/assets/20f5bdc4-2a3b-41c0-8d24-47e717a3294c" />


I aquest és el contingut.
He cambiat la contrasenya a marc1234.

<img width="718" height="106" alt="image" src="https://github.com/user-attachments/assets/d580c5ce-7bc5-46c0-a194-5c2763762a03" />

I apliquem el fitxer al servidr ldap.

<img width="914" height="85" alt="image" src="https://github.com/user-attachments/assets/4633f38a-d8fc-439a-b8a4-695c05cfc52e" />

## ldapdelete 

Ldapdelete no necessita cap fitxer de configuració nou podem aplicar la comanda directament.

<img width="1088" height="100" alt="image" src="https://github.com/user-attachments/assets/655a69a2-56d5-4771-9756-6ba20ed20980" />

## CONFIGURACIÓ LDAP ENTORN GRÀFIC

En primer lloc instal·lare al servidor l'eina d'etorn gràfic per configurar ldap.

<img width="1053" height="524" alt="image" src="https://github.com/user-attachments/assets/6ee5d35b-d60d-4e2c-b59c-2467b35f4735" />

<img width="327" height="214" alt="image" src="https://github.com/user-attachments/assets/3fad02a2-2acd-43ae-8750-d0f7e074b5c1" />

És necessari instal·lar java per iniciar apache.

<img width="865" height="328" alt="image" src="https://github.com/user-attachments/assets/b5c8a432-c935-4f9d-ab23-e24fd22504a6" />







