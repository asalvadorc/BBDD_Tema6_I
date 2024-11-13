# Objectius i Coneixements previs

![](icon_objectives.gif)

## Objectius

L'objectiu primordial és **dominar el llenguatge SQL** , per a poder fer
sentències de dificultat mitjana-alta. En particular s'hauran de saber fer:

  * Consultes DDL per a crear, modificar i esborrar taules i vistes.
  * Consultes DML per a inserir, modificar o esborrar files d'una taula.
  * Consultes SELECT, per a traure informació de les taules. Concretament s'haurà de conéixer a la perfecció totes les seues clàusules.
  * Consultes SELECT amb combinacions o reunions de taules, incloent les combinacions externes (LEFT JOIN).
  * Consultes d'unió
  * Subconsultes

Un altre objectiu és el de conèixer l'arquitectura**client-servidor** , i per
a aconseguir açò treballarem en **PostgreSQL**. Mentre que en **Access**
cadascú tenia la seua pròpia Base de Dades, ara en PostgreSQL la Base de Dades
està en un únic lloc remot, en el servidor. I tots ens connectem com a usuaris
al servidor (com a clients). Per ser més conscients, ens connectarem com el
mateix usuari a la mateixa Base de Dades, compartint per tant les dades,
excepte quan ens toque crear objectes, que cadascú es connectarà com un usuari
diferent a una Base de Dades diferent, per a no interferir els uns amb els
altres.

Per l'extensió del tema, el dividirem en 3 parts.

  * Per motius didàctics començarem per la sentència SELECT, en la seua forma més senzilla.
  * Continuarem amb les consultes més complicades del SELECT.
  * Per últim veurem les sentències DDL i les de manipulació de dades.

![](icon_preknowledge.gif)

## Coneixements previs

Els coneixements previs estrictes del tema és el Model Relacional, encara que
no el podrem deslligar de tot l'entorn que ens estem construint a l'hora de
dissenyar una Base de Dades, i així el tema del Model Entitat-Relació també
ens vindrà molt bé. I per a poder practicar ens fa falta un SGBD. S'ha optat
per un SGBD nou no vist encara, **PostgreSQL** , pel comentat en el punt
anterior. Com és la primera vegada que es veu, no hi ha coneixements previs de
cap entorn d'aquest SGBD.


Llicenciat sota la  [Llicència Creative Commons Reconeixement NoComercial
CompartirIgual 3.0](http://creativecommons.org/licenses/by-nc-sa/3.0/)

