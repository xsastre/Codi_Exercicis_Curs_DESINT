!!!info **Consell per a l'alumne:**
Si l'informe genera milers de pàgines (Sakila té molts lloguers), recomana'ls afegir un LIMIT 100 a la consulta SQL mentre estiguin fent proves de disseny.

## Bloc 0: Exercicis bàsics amb Jasper Studio

### Exercici 1: Informe bàsic

L'objectiu d'aquesta pràctica és crear un document PDF que mostri un llistat de comandes utilitzant la **Sample DB** (base de dades de prova) de Jaspersoft.

Pots consultar aquí la solució passa a passa:  [Exercici 1 amb Jasper Studio - Solució pas a pas](Exercici 1 Primer informe amb JasperSoft Studio.md)

### Exercici 2: Informe de productes.

Utilitzant la mateixa base de dades de prova (Sample DB), l'alumne ha de crear un informe des de zero amb els següents requisits:

- Origen de dades: Taula PRODUCT.
- Camps a mostrar: ID del producte, Nom del producte i Preu de venda.
- Requisit de disseny 1: L'informe ha de tenir una capçalera de pàgina amb la data actual (utilitza l'element "Current Date" de la paleta).
- Requisit de disseny 2: Els títols de les columnes han d'estar en negreta i amb un fons de color gris clar.
- Requisit de format: El preu ha d'aparèixer alineat a la dreta.

Objectiu: Demostrar autonomia en la selecció de taules i format bàsic de cel·les.


## Bloc 1: Complexitat en Consultes i Lògica (Sample DB)

### Exercici 3: Informe de Vendes amb Agrupacions

**Objectiu:** Aprendre a utilitzar els _Groups_ de Jasper per organitzar dades.

- **Consulta SQL:** `SELECT * FROM ORDERS ORDER BY SHIPCOUNTRY`
    
- **Enunciat:** Crea un informe que llisti les comandes, però agrupades per país d'enviament (`SHIPCOUNTRY`).
    
- **Requisits:**
    
    - Crea un **Group** basat en el camp `SHIPCOUNTRY`.
        
    - Mostra el nom del país només a la capçalera del grup (_Group Header_).
        
    - Afegeix un recompte total de comandes per cada país al peu del grup (_Group Footer_) utilitzant una **Variable**.
        

### Exercici 4: Càlculs i Formats Condicionals

**Objectiu:** Ús d'expressions Java i estils condicionals.

- **Consulta SQL:** `SELECT * FROM ORDERS WHERE FREIGHT > 0`
    
- **Enunciat:** Llista les comandes mostrant l'ID, el cost de transport (`FREIGHT`) i una nova columna inventada anomenada "Transport amb IVA" (calcula el 21% sobre el `FREIGHT`).
    
- **Requisits:**
    
    - Si el cost del transport és superior a 100, el text del preu ha d'aparèixer en **vermell**.
        
    - Utilitza una expressió ternària en un `TextField` per mostrar el text "URGENT" si el camp `SHIPREGION` és nul.
        



## Bloc 2: Nous Orígens de Dades

### Exercici 5: Connexió a fitxer CSV extern

**Objectiu:** Aprendre que Jasper no només llegeix SQL.

- **Nou Origen de Dades:** Crea un _Data Adapter_ de tipus **CSV File**. (L'alumne haurà de crear prèviament un fitxer `.csv` simple amb columnes com `Nom`, `Cognom`, `Edat`).
    
- **Enunciat:** Crea un informe tipus "Llistat de socis" que llegeixi directament del fitxer CSV.
    
- **Requisits:** Configurar correctament els separadors (comes o punts i coma) i fer que la primera fila es llegeixi com a capçalera.
    

### Exercici 6: Connexió a Base de Dades Externa (PostgreSQL/MySQL)

**Objectiu:** Configurar controladors JDBC.

- **Nou Origen de Dades:** Configura un _Data Adapter_ per connectar-te a una base de dades externa (pot ser una instal·lació local de MySQL o PostgreSQL).
    
- **Enunciat:** Realitza una consulta `JOIN` complexa entre dues taules (per exemple, `Clients` i `Factures`).
    
- **Requisits:** Importar el controlador `.jar` corresponent si Jasper no el porta per defecte.
    



## Bloc 3: Informes Avançats (Productivitat i Gràfics)

### Exercici 7: Ús de Paràmetres (Informes Dinàmics)

**Objectiu:** Filtrar dades en temps d'execució.

- **Consulta SQL:** `SELECT * FROM ORDERS WHERE ORDERDATE BETWEEN $P{DataInici} AND $P{DataFi}`
    
- **Enunciat:** Crea un informe on l'usuari hagi d'introduir dues dates abans de veure el resultat.
    
- **Requisits:** Defineix dos **Parameters** (`DataInici` i `DataFi`) de tipus `java.util.Date`. L'informe només ha de mostrar les comandes d'aquell rang.
    

### Exercici 8: Subinformes (Informes niats)

**Objectiu:** Mostrar dades de diferents taules relacionades en un sol document.

- **Enunciat:** Crea un informe principal de "Clients" i, dins de la banda _Detail_, insereix un **Subreport** que mostri les dades de les "Comandes" d'aquell client concret.
    
- **Requisits:** Configurar la connexió del subinforme perquè utilitzi la mateixa que el principal i passar l'ID del client com a vincle entre ambdós.
    



## Bloc 4: Visualització Professional

### Exercici 9: Gràfics Estadístics (Charts)

**Objectiu:** Convertir dades numèriques en visuals.

- **Consulta SQL:** `SELECT SHIPCITY, SUM(FREIGHT) as TOTAL FROM ORDERS GROUP BY SHIPCITY LIMIT 10`
    
- **Enunciat:** Crea un informe que mostri un **Gràfic de Barres** (Chart) amb el total de vendes per ciutat.
    
- **Requisits:** Configurar el _Dataset_ del gràfic correctament definint l'eix X (Categories) i l'eix Y (Valors).
    

### Exercici 10: Informe Mestre amb Codis de Barres i QR

**Objectiu:** Generar documents industrials.

- **Enunciat:** Crea una "Etiqueta d'Enviament".
    
- **Requisits:** * Dissenya un informe amb una mida de pàgina personalitzada (per exemple, 10cm x 15cm).
    
    - Inclou un element **Barcode** que codifiqui l'`ORDERID`.
        
    - Inclou un element **QR Code** que contingui una URL fictícia de seguiment amb les dades de la comanda.

### Exercici 11 Jasper - Informe complexe amb bd sakila.

Objectiu: Crear un informe mestre-detall que mostri la informació de cada client de la videoteca i, just a sota, la llista de pel·lícules que ha llogat.

Dissenya un informe a Jaspersoft Studio utilitzant la connexió a **MariaDB (Sakila)** amb els següents requeriments:

- **Estructura d'Agrupació:** L'informe ha d'estar agrupat per `customer_id`.
    
- **Capçalera de Grup (Dades del Soci):**
    
    - Mostra el nom complet del soci en majúscules (utilitza una expressió Java: `$F{first_name}.toUpperCase() + " " + $F{last_name}.toUpperCase()`).
        
    - Mostra el correu electrònic en un color blau i subratllat (estil de link).
        
- **Banda de Detall (Històric):**
    
    - Per a cada soci, llista la data del lloguer i el títol de la pel·lícula.
        
    - Si un soci no ha llogat mai cap pel·lícula, ha d'aparèixer el text "Sense lloguers registrats" (ajuda: usa _Print When Expression_ o una expressió ternària).
        
- **Càlculs (Peu de Grup):**
    
    - Crea una **Variable** que compti quants lloguers ha fet cada soci i mostra el total al final de cada grup.
        
- **Estètica:**
    
    - Dibuixa una línia horitzontal o un rectangle que separi un soci del següent per millorar la llegibilitat.

### Exercici 12: Integració de JasperReports en Java.

L'objectiu d'aquesta pràctica és desenvolupar una aplicació Java que automatitzi la generació d'un informe prèviament dissenyat (com el de l'Exercici 11) i l'exporti directament a format PDF.

**Requisits de l'exercici:**

- **Projecte Maven:** Configura un projecte Maven amb les dependències necessàries per a JasperReports i el connector JDBC de MariaDB.
- **Connexió JDBC:** Implementa una connexió segura a la base de dades Sakila.
- **Flux de treball Jasper:**
    - **Compilació:** Carrega i compila el fitxer `.jrxml`.
    - **Emplenat (Fill):** Omple l'informe amb les dades de la base de dades (i paràmetres si n'hi hagués).
    - **Exportació:** Desa el resultat final en un fitxer anomenat `Informe_Sakila_Socis.pdf`.
- **Robustesa:** El codi ha d'incloure una gestió correcta d'excepcions (`try-catch-finally`) per tancar la connexió a la base de dades i gestionar possibles errors de Jasper.

Pots consultar aquí el codi font i la configuració del projecte: [Exercici 12 - Solució Codi Java](Solucions_Jasper/Ex12_codi.md)

---

## Bloc Extra: Exercicis de Preparació per a l'Examen

### Exercici 13: SQL, Paràmetres i Expressions Java
**Objectiu:** Practicar el filtratge, la lògica de dades i el format condicional.

**Enunciat:** Dissenya un informe que llisti les pel·lícules de la base de dades Sakila.
1. **SQL**: Crea una consulta que obtingui el títol, la durada (`length`) i el cost de reemplaçament (`replacement_cost`).
2. **Paràmetre**: Afegeix un paràmetre `p_titol` per filtrar les pel·lícules que continguin una cadena de text específica (ús de `LIKE`).
3. **Expressió Java (Càlcul)**: El camp `length` està en minuts. Crea una expressió Java per mostrar-ho en format "Xh Ym" (Ex: 130 min -> 2h 10m).
4. **Format Condicional**: Si el `replacement_cost` és superior a 25.00, el text del preu ha de sortir en **verd i negreta**.
5. **Resum**: Afegeix una variable al `Summary` que calculi la mitjana de durada de les pel·lícules mostrades.

### Exercici 14: Estructura Mestre-Detall (Subinformes)
**Objectiu:** Practicar la vinculació d'informes i l'agrupació complexa.

**Enunciat:** Crea un informe de "Països i Ciutats".
1. **Informe Principal**: Consulta la taula `country`. Mostra el nom del país.
2. **Subinforme**: Crea un informe que llisti les ciutats (`city`) d'un país determinat.
3. **Vinculació**: Passa el `country_id` des de l'informe principal al subinforme.
4. **SQL Subinforme**: La consulta del subinforme ha de filtrar per l'ID rebut.
5. **Estètica**: Cada país ha de començar en una pàgina nova (ús de *Break* o *Group* amb *Start on a new page*) i tenir una capçalera clara.


### Exercici 15: Integració amb Java i Interfície Gràfica
**Objectiu:** Practicar la càrrega de Jasper des de codi i la creació d'una UI funcional.

**Enunciat:** Crea una aplicació Java (Swing o JavaFX) per gestionar un informe simple de clients.
1. **Informe**: Crea un informe molt simple (`clients.jrxml`) que llisti els clients d'una botiga (`store_id`).
2. **UI Java**:
    - Un camp de text o selector per indicar l'`ID de la botiga`.
    - Un botó "Generar Informe".
    - Un botó "Seleccionar Destí" que obri un `JFileChooser` per triar on desar el PDF.
3. **Codi**:
    - Implementa la connexió JDBC.
    - En fer clic a "Generar", el programa ha de compilar el `.jrxml` (o carregar el `.jasper`), passar-li el paràmetre de la botiga i exportar-lo a la ruta triada.
4. **Gestió d'errors**: Si la base de dades no està activa o la ruta no és vàlida, mostra un `JOptionPane` amb un missatge d'error entenedor.

---

### Checklist de Repàs Final
Abans de l'examen, assegura't que saps:
- [ ] Fer `JOIN` entre 3 o més taules.
- [ ] Usar `GROUP_CONCAT` per llistar dades relacionades en una sola cel·la.
- [ ] Passar paràmetres de Java a Jasper.
- [ ] Passar paràmetres de l'informe mestre al subinforme.
- [ ] Configurar el `SUBREPORT_DIR` perquè Jasper trobi els fitxers `.jasper`.
- [ ] Fer servir `JasperExportManager.exportReportToPdfFile`.
