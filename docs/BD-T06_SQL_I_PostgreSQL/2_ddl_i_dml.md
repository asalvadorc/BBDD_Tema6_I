# 2\. DDL i DML

Com s'ha comentat en la pregunta anterior, SQL ens permet definir, controlar i
accedir a una Base de Dades.

Farem una distinció principal entre aquestes funcions, separant el que són les
estructures de les taules i el contingut de les taules. En aquest sentit
tindrem 2 subtipus de llenguatges:

  * **DDL** (_Data Definition Language_ o _Llenguatge de Definició de Dades_): permet definir, modificar o esborrar les estructures, com poden ser taules, vistes, índex, ... i fins i tot Bases de Dades. Bàsicament les sentències són 3:   


  |    |    |     
---|---  
**CREATE** | per a crear l'estructura   
**ALTER** | per a modificar-la  
**DROP** | per a esborrar-la  


  * **DML** (_Data Manipulation Language_ o _Llenguatge de Manipulació de Dades_): permet accedir al contingut de les estructures, a les dades. Aquest accés pot ser de dos tipus: per a consultar o per a modificar les dades   
  
Per a consultar:  
**SELECT**  
  
Per a modificar  

  |    |    |     
---|---  
**INSERT** | insereix noves files  
**UPDATE** | modifica el contingut de files ja existents  
**DELETE** | esborra files  

El llenguatge SQL és més extens que les sentències anteriors, incorporant
també el que s'anomena **DCL** (_Data Control Language_ o _Llenguatge de
Control de Dades_), que permet controlar les dades per a donar permisos o
llevar-los sobre les dades, o controlar les transaccions, ..., però de moment
ens aconformarem amb les sentències de DML i DDL, i aquestes últimes,
sobretot, per a definir taules.



Llicenciat sota la  [Llicència Creative Commons Reconeixement NoComercial
CompartirIgual 3.0](http://creativecommons.org/licenses/by-nc-sa/3.0/)

