# 7\. Funcions

Com veurem un poc més avant, en les sentències SQL, a banda de columnes i
valors constants, podrem utilitzar funcions.

PostgreSQL té moltes funcions ja creades.

Farem un recull de les funcions més importants de PostgreSQL, d'entre la
multitud de funcions que existeixen. Les agruparem per categories.

Evidentment aquest recull no és per aprendre'l de memòria, sinó que servirà de
consulta.

Funcions numèriques

Funció  |  Explicació  |  Funció  |  Explicació   
---|---|---|---  
ABS(n) |  Valor absolut de n. |  LOG(m,n) |  Logaritme, base m, de n  
ACOS(n) |  Arccosinus de n (invers del cosinus) |  MOD(m,n) |  La resta de la divisió entre m i n  
ASIN(n) |  Arcsinus de n (invers de sinus) |  POWER(m,n) |  m elevat a n  
ATAN(n) |  Arctangent de n (invers de la tangent) |  RANDOM() |  número aleatori entre 0 i 1  
CEIL(n) |  Enter immediatament superior o igual a n |  Round(n,[m]) |  n arrodonit a m xifres decimals  
(per defecte 0)  
COS(n) |  Cosinus de n. |  SIN(n) |  Sinus de n  
EXP(n) |  Exponencial de n (en) |  SQRT(n) |  Arrel quadrada de n  
FLOOR(n) |  Enter immediatament inferior o igual a n |  TAN(n) |  Tangent de n  
LN(n) |  Logaritme neperià de n |  Trunc(n,[m]) |  n truncat a m xifres decimals  
(per defecte 0)  
  
Per exemple, podríem simular el llançament d'un dau d'aquesta manera:

SELECT TRUNC(RANDOM()*6+1);

Funcions de caràcters

Funció  |  Explicació  |  Funció  |  Explicació   
---|---|---|---  
ASCII(c) |  Torna el codi ASCII corresponent al caràcter c |  REPLACE(c1,c2,c3) |  Reemplaça en **c1** cada ocurrència de **c2** per **c3**  
CHR(n) |  Torna el caràcter amb codi ASCII n. |  RPAD(c1,n[c2]) |  Torna **c1** reomplida per la dreta fins **n** caràcters amb la cadena **c2**  
CONCAT(c1,c2) |  Concatena les dues cadenes (equivalent a l'operador ||) |  RTRIM(c1[,set]) |  Retalla per la dreta mentre troba la cadena set (per defecte blancs)  
INITCAP(c1) |  Torna la cadena amb la primera lletra de cada paraula en majúscules, i les altres en minúscules |  STRPOS(s,s1) |  Busca la primera ocurrència de la subcadena s1 dins de la cadena s  
LENGTH(c1) |  Llargària de la cadena. Si c1 és de tipus CHAR, inclourà tots els espais en blanc del final. |  SUBSTR(c1,m[,n]) |  Torna una subcadena de c1 que comença en el caràcter m i consta de n caràcters (per defecte fins el final)  
LPAD(c1,n[c2]) |  Torna c1 reomplida per l’esquerra fins n caràcters amb la cadena c2 |  TRANSLATE(c1,c2,c3) |  Torna c1 amb cada caràcter de c2 substituït pel corresponent (en ordre) de c3.  
LTRIM(c1[,set]) |  Retalla per l’esquerra mentre troba la cadena set (per defecte blancs) |  LOWER(c1) |  Torna la cadena en minúscules  
UPPER(c1) |  Torna la cadena en majúscules  
  
Per exemple, traurem els graus de la latitud de les poblacions. Haurem
d'agafar els 2 primers caràcters (els de l'esquerra).

SELECT nom , latitud , SUBSTR(latitud,1,2)  
FROM POBLACIONS;

Açò ho podríem millorar, ja que d'aquesta manera obliguem a que siguen sempre
dos caràcters, els graus. De forma més genèrica, els graus és el que va davant
del símbol **º**. Per tant el que podem fer és buscar aquest símbol i traure
els de davant (des del primer fins a l'anterior a ell)

SELECT nom , latitud , SUBSTR(latitud,1,STRPOS(latitud,'º')-1)  
FROM POBLACIONS;

Per agafar els minuts de forma senzilla seria traure els caràcters 4t i 5è, és
a dir, 2 caràcters a partir del 4.

SELECT nom , latitud , SUBSTR(latitud,4,2)  
FROM POBLACIONS;

Però de forma més genèrica (per si no s'han posat 0 no significatius), haurem
de traure des de després del símbol **º** fins al caràctar anterior a **'**
(la cometa) que assenyala els minuts. Tenim a més la dificultat afegida que la
cometa justament és la manera d'especificar un text en SQL. Haurem de posar
dos cometes per a escapar, i com que és un text va entre cometes. Resultat: 4
cometes.

SELECT nom , latitud ,
SUBSTR(latitud,STRPOS(latitud,'º')+1,STRPOS(latitud,'''')-STRPOS(latitud,'º')-1)  
FROM POBLACIONS;

I el mateix faríem per als segons, (entre la cometa simple i la doble).

Aquesta sentència resumeix l'anterior, separant graus, minuts i segons.

SELECT nom, latitud,  
SUBSTR(latitud,1,STRPOS(latitud,'º')-1),  
SUBSTR(latitud,STRPOS(latitud,'º')+1,STRPOS(latitud,'''')-STRPOS(latitud,'º')-1),  
SUBSTR(latitud,STRPOS(latitud,'''')+1,STRPOS(latitud,'"')-STRPOS(latitud,'''')-1)  
FROM POBLACIONS;

Funcions de data

Funció |  Explicació  
---|---  
NOW() (CURRENT_TIMESTAMP) |  Torna la data-hora actual, amb la diferència d'hores respecte la GMT |  Totes les funcions que tornen hores (amb data o sense), ho faran fins la micra de segon, a no ser que entre parèntesi indiquem les xifres decimals (de segon) que volem  
LOCALTIMESTAMP |  Igual que l'anterior, però sense la diferència de la GMT  
CURRENT_DATE |  Torna la data actual  
CURRENT_TIME |  Torna l'hora actual (amb diferència GMT)  
LOCALTIME |  Torna l'hora actual (sense diferència GMT)  
AGE(t) |  Torna la diferència de la data actual i t  
AGE(t1,t2) |  Torna la diferència entre t1 (posterior) i t2 (anterior)  
EXTRACT(camp FROM t) |  Trau el número corresponent al camp (que pot ser year, month, day, hour, minute, second, millisecond, microsecond, dow (day of week), ...  
  
Per exemple, ¿quan de temps ha passat des de l'intent de cop d'estat?

SELECT AGE('1981/02/23'::DATE);

O un altre, ¿en quin any estem?

SELECT EXTRACT(year FROM CURRENT_DATE);

Funcions geomètriques

Funció |  Explicació |  Funció |  Explicació  
---|---|---|---  
AREA(o) |  Àrea de l'objecte |  HEIGTH(r) |  Altura del rectàngle  
CENTER(o) |  Centre de l'objecte |  RADIUS(c) |  Radi del cercle  
DIAMETER(c) |  Diàmetre del cercle |  WIDTH(r) |  Amplària del rectàngle  
  
Per exemple, l'àrea d'un cercle:

SELECT AREA('((5,5),2)'::CIRCLE);

Funcions IP

Funció |  Explicació |  Exemple |  Resultat  
---|---|---|---  
HOST(ip) |  Trau en format text l'adreça IP |  HOST('192.168.2.15/24') |  192.168.2.15  
MASKLEN(ip) |  Trau el número de bits de la màscara |  MASKLEN('192.168.2.15/24') |  24  
SET_MASKLEN(ip,n) |  Posa el número de bits de la màscara als especificats |  SET_MASKLEN('192.168.2.15/24',16) |  192.168.2.15/16  
NETMASK(ip) |  Construeix la màscara de xarxa |  NETMASK('192.168.2.15/24') |  255.255.255.0  
  
Funcions de conversió

Serviran per a passar d'un tipus a un altre, on un d'ells serà el tipus de
cadena (VARCHAR)

Funció |  Explicació  
---|---  
**TO_CHAR(_data, format_)** |  Converteix una data en una tira de caràcters, utilitzant el format especificat (es veurà aquest format en la següent pregunta)  
**TO_CHAR(_número, format_)** |  Converteix un número en una tira de caràcters  
**TO_NUMBER(_exp., format_)** |  Converteix una tira de caràcters en un número, suposant que estava en el format indicat  
**TO_DATE(_exp., format_)** |  Converteix una tira de caràcters en un data  
**TO_DATETIME(_exp., format_)** |  converteix una tira de caràcters en un data-hora  
  
## 7.1 Formats de les dates

Aquest tipus és molt versàtil en quant al format, bé siga per a la introducció
de les dades, o el que és més habitual, per a la seua presentació. S'haurà
d'utilitzar una funció, **TO_CHAR** , que acceptarà 2 paràmetres: el primer la
data que es vol presentar, i el segon el format que volem. En el format
indicarem per mig de determinats caràcters l'aspecte que volem. Per exemple,
per a traure la data d'avui amb el format dia-mes-any, posaríem:

SELECT TO_CHAR( NOW(), 'DD-MM-YYYY');

El següent quadre resumeix aquestos caràcters, agrupat per categories:

**DIES** |  **MESOS** |  **ANYS**  
---|---|---  
**D** | Dia de la setmana (1-7) | **MM** | Mes (1-12) | **Y** | Últim dígit de l'any  
**DD** | Dia del mes (1-31) | **MONTH** | Mes en lletres, utilitzant 9 caràcters | **YY** | Últims 2 dígits de l'any  
****DDD**** | Dia de l'any (1-366) | **MON** | Mes abreviat, utilitzant 3 caràcters | **YYY** | Últims 3 dígits de l'any  
****DAY**** | Dia de la setmana en lletres, utilitzant 9 caràcters | **RM** | El mes amb números romans (juliol= VII) | **YYYY** | Any amb 4 dígits  
****DY**** | Dia de la setmana abreviat, utilitzant 3 caràcters |  |  | **** |   
  
En principi els formats que tornen lletres ho estaran en anglès, però després
veurem com canviar d'idioma.

**HORES** |  **MINUTS** |  **SEGONS**  
---|---|---  
**HH , HH12** | Hora (1-12) |  **MI** | Minuts | **SS** | Segons  
**HH24** | Hora (0-23) |  |  | **SSSS** | Segons des de la mitjanit (0-86399)  
**PM , AM  
** | Abans o després del migdia (AM i PM respectivament) |  |  |  |   
  
**ALTRES**  
---  
**W , WW** | Setmana del mes (1-5) ; Setmana de l'any (1-53) |  **CC** | Segle, amb 2 xifres |  **Q** | Quart d'any, trimestre (1-4)  
**/ , . ; : -**  
** <espai en blanc> **  
**"text"** | Caràcters que poden aparèixer acompanyant. | En els formats que tornen lletres, poden eixir en majúscules, minúscules o la primera en majúscula, si així ho posem en les lletres del format.  
Si immediatament davant d'un format que torna lletres posem **FM** , eixiran
els caràcters justos que ocupen (per exemple el dia de la setmana o el mes), i
en els numèrics no eixiran els 0 no significatius.  
Si immediatament davant d'un format que torna lletres posem **TM** , ho
traduirà a l'idioma que estiga configurat el servidor, però com el tenim
configurat en anglès el resultat serà el mateix  
  
Exemples:

Si ara fóra **9/1/16 13:39** (en el servidor, no en la vostra màquina), i
férem **SELECT TO_CHAR(NOW(),'_format_****');**

Format |  Eixida  
---|---  
dd-mm-yy hh:mi | **09-01-23 01:39**  
dd-mm-yy hh24:mi | **09-01-16 13:39**  
dd-MON-yyy | **09-JAN-023**  
dd-TMMON-yyy | **09-ENE-023 _(si el tinguérem configurat en espanyol)_**  
Day, dd "de" month "de" yyyy | **Monday , 09 de january de 2023 de 2016**  
FMDay, dd "de" FMmonth "de" yyyy. | **Monday, 09 de january de 2023.**  
TMDay, dd "de" TMmonth "de" yyyy. | **Lunes, 09 de enero de 2023.**_(si el tinguérem configurat en espanyol)_  
FMDy PM FMhh-FMmi-FMss | **Mon PM 1-39-00**  
TMDy PM TMhh-TMmi-TMss | **Lun PM 01-39-00 __**_(si el tinguérem configurat en espanyol)_  

## 7.2 Formats dels números


També podrem utilitzar la funció **TO_CHAR** per a donar l'aspecte que vulguem
als números. En la següent taula tenim un resum amb els diferents símbols, un
comentari descriptiu de cada símbol, i un exemple de format amb el resultat
que donaria per a un determinat valor. La sentència seria **SELECT
TO_CHAR(**_valor_**,'**_format_**');** :

### Símbol

|

### Comentari

|

### Format

|

### Valor

|

### Resultat  
  
---|---|---|---|---  
**9** |  Equival a una xifra decimal. Torna el valor amb el número de xifres especificades, substituint els zeros no significatius per espais en blanc. Únicament no substitueix per espais en blanc quan el valor és 0. Els negatius els treu amb el signe, i els positius sense.  |  **9999** |  34  
-34  |  34  
-34   
**0** |  Igual a l'anterior, però sense substituir els zeros no significatius per espais en blanc.  |  **0000** |  34  
-34  |  0034  
-0034   
**S** |  Treu el signe: - per als negatius, + per als positius.  |  **S9990** |  34  
-34  |  +34  
-34   
**$** |  Treu aquest símbol.  |  **$9990** |  34  |  $ 34   
**.** |  Treu el punt decimal en la posició indicada  |  **9990.99**  
  
**9999.99** |  34  
0.5  
0.5  |  34.00  
0.50  
.50  
**,** |  Treu la coma separadora de milers  | **9,999,990.99** |  34  
1234.5  
1234567  |  34.00  
1,234.50  
1,234,567.00  
**€**  
|  Treu el símbol monetari de l'euro  |  **9990€** |  34  |  34€   
**D** |  Treu el símbol separador de la part decimal del país  |  **9990D99** |  34  
0.5  |  34,00  
0,50  
**G** |  Treu el símbol separador dels milers del país en la posició indicada  |  **9G999G990D99**  
  
**9G990D99** |  1234  
1234567  
1234.5  |  1.234,00  
1.234.567,00  
1.234,50  
**RN** |  Treu el valor en números romans (fins el 3999).  |  **RN**  
**rn** |  1967  |  MCMLXVII  
mcmlxvii  

Llicenciat sota la  [Llicència Creative Commons Reconeixement NoComercial
CompartirIgual 3.0](http://creativecommons.org/licenses/by-nc-sa/3.0/)

