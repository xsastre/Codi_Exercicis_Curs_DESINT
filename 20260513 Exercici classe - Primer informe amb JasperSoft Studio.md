
L'objectiu d'aquesta pràctica és crear un document PDF que mostri un llistat de comandes utilitzant la **Sample DB** (base de dades de prova) de Jaspersoft.

### Pas 1: Iniciar el projecte i l'assistent d'informes

1. Obre **Jaspersoft Studio**.
    
2. Al menú superior, fes clic a **File** > **New** > **Jasper Report**.
    
3. S'obrirà l'assistent ("Report Wizard"). Selecciona la plantilla **Blank A4** (A4 en blanc) i fes clic a **Next**.
    
4. Dóna un nom al teu fitxer, per exemple `Informe_Test.jrxml`, i assegura't de desar-lo dins de la teva carpeta de projecte principal (habitualment anomenada "MyReports"). Fes clic a **Next**.
    

### Pas 2: Configurar la connexió a la base de dades

1. A la finestra "Data Source", obre el menú desplegable superior anomenat "Data Adapter".
    
2. Selecciona **Sample DB** (aquesta és una base de dades de prova que s'instal·la automàticament amb l'entorn de treball).
    
3. A l'espai de text buit que hi ha a sota, escriu la següent consulta SQL per obtenir les dades de les comandes:
    
    `SELECT * FROM ORDERS`
    
4. Un cop escrita la consulta, fes clic a **Next**.
    

### Pas 3: Seleccionar els camps a mostrar

1. A la part esquerra de la pantalla, veuràs una llista amb tots els camps disponibles a la taula ORDERS (ORDERID, CUSTOMERID, FREIGHT, SHIPCITY, etc.).
    
2. Selecciona els camps `ORDERID`, `CUSTOMERID`, `SHIPCITY` i `FREIGHT`. Pots fer-ho fent doble clic a cadascun o seleccionant-los i prement el botó de la fletxa simple ( **>** ). Aquests camps passaran a la llista de la dreta.
    
3. Fes clic a **Next**.
    
4. La següent pantalla serveix per agrupar dades ("Group By"). Per mantenir aquest test senzill, no hi farem res. Fes clic directament a **Finish**.
    

### Pas 4: Dissenyar l'aspecte de l'informe

Ara se t'haurà obert l'espai de treball principal. Veuràs que el document està dividit en franges horitzontals anomenades "Bandes" (Title, Page Header, Column Header, Detail, etc.).

1. **Afegir un títol:** Ves a la finestra **Palette** (habitualment a la dreta). Fes clic a l'element **Static Text** i arrossega'l cap a dins de la banda **Title**. Fes doble clic sobre el text i escriu "Llistat de Comandes de Prova". Pots fer el text més gran o posar-lo en negreta des de la pestanya _Properties_.
    
2. **Afegir les dades:** A la finestra **Outline** (habitualment a l'esquerra), expandeix la carpeta **Fields**. Allà hi veuràs els camps que hem seleccionat al pas anterior.
    
3. Selecciona tots quatre camps alhora (pots fer-ho prement la tecla Ctrl o Shift) i arrossega'ls cap a la banda **Detail 1**.
    
4. Jaspersoft Studio farà dues coses automàticament: col·locarà els títols de les columnes a la banda **Column Header** i els textos dinàmics de les dades a la banda **Detail 1**. Ajusta'n l'amplada i la posició amb el ratolí perquè quedin alineats i no se superposin.
    

### Pas 5: Previsualitzar i compilar

1. A la part inferior de la zona central de disseny, veuràs tres pestanyes: **Design**, **Source** i **Preview**.
    
2. Fes clic a la pestanya **Preview**.
    
3. El programa compilarà el disseny, executarà la consulta SQL a la base de dades i et mostrarà com queda l'informe ple de dades reals.
    
4. Si veus que alguna columna queda tallada o el disseny no t'agrada, torna a la pestanya **Design**, fes els ajustos necessaris amb el ratolí, i torna a fer clic a **Preview** per actualitzar la vista.
    

### Pas 6: Exportar el resultat final

1. Dins de la mateixa pestanya de **Preview**, fixa't en la petita barra d'eines que hi ha just a sobre de l'informe generat.
    
2. Busca la icona d'exportació (sol tenir forma de document amb una fletxa verda o bé un menú desplegable amb un disquet).
    
3. Selecciona **Export to PDF**.
    
4. Tria a quina carpeta del teu ordinador vols desar el fitxer i fes clic a **Save**.