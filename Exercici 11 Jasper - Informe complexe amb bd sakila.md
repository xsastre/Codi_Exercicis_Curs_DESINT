
## Llistat de Socis amb Històric de Lloguers

**Objectiu:** Crear un informe mestre-detall que mostri la informació de cada client de la videoteca i, just a sota, la llista de pel·lícules que ha llogat.

### 1. Preparació de la consulta SQL

Per aquest exercici, necessitarem fer un `JOIN` entre les taules `customer`, `rental`, `inventory` i `film`.

**Consulta suggerida:**

SQL

```
SELECT 
    c.customer_id, 
    c.first_name, 
    c.last_name, 
    c.email, 
    r.rental_date, 
    f.title AS film_title
FROM customer c
LEFT JOIN rental r ON c.customer_id = r.customer_id
LEFT JOIN inventory i ON r.inventory_id = i.inventory_id
LEFT JOIN film f ON i.film_id = f.film_id
ORDER BY c.last_name, c.customer_id, r.rental_date DESC
```

### 2. Enunciat per a l'alumne

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
        

---

### 3. Solució en format JRXML (Codi font)

Pots copiar aquest codi per verificar l'estructura. He netejat els UUIDs perquè no tinguis errors de versió.

XML

```
<?xml version="1.0" encoding="UTF-8"?>
<jasperReport xmlns="http://jasperreports.sourceforge.net/jasperreports" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://jasperreports.sourceforge.net/jasperreports http://jasperreports.sourceforge.net/xsd/jasperreport.xsd" name="Sakila_Soci_Historic" pageWidth="595" pageHeight="842" columnWidth="555" leftMargin="20" rightMargin="20" topMargin="20" bottomMargin="20">
    <property name="com.jaspersoft.studio.data.defaultdataadapter" value="MariaDB Sakila"/>
    <queryString language="SQL">
        <![CDATA[SELECT c.customer_id, c.first_name, c.last_name, c.email, r.rental_date, f.title 
                 FROM customer c 
                 LEFT JOIN rental r ON c.customer_id = r.customer_id 
                 LEFT JOIN inventory i ON r.inventory_id = i.inventory_id 
                 LEFT JOIN film f ON i.film_id = f.film_id 
                 ORDER BY c.last_name, c.customer_id]]>
    </queryString>
    <field name="first_name" class="java.lang.String"/>
    <field name="last_name" class="java.lang.String"/>
    <field name="email" class="java.lang.String"/>
    <field name="rental_date" class="java.sql.Timestamp"/>
    <field name="title" class="java.lang.String"/>
    
    <group name="SociGroup">
        <groupExpression><![CDATA[$F{email}]]></groupExpression>
        <groupHeader>
            <band height="50">
                <textField>
                    <reportElement x="0" y="10" width="300" height="20" forecolor="#2C3E50"/>
                    <textElement><font size="12" isBold="true"/></textElement>
                    <textFieldExpression><![CDATA[$F{first_name}.toUpperCase() + " " + $F{last_name}.toUpperCase()]]></textFieldExpression>
                </textField>
                <textField>
                    <reportElement x="0" y="30" width="300" height="15" forecolor="#2980B9"/>
                    <textElement><font isUnderline="true"/></textElement>
                    <textFieldExpression><![CDATA[$F{email}]]></textFieldExpression>
                </textField>
            </band>
        </groupHeader>
    </group>
    
    <detail>
        <band height="20">
            <textField isBlankWhenNull="true">
                <reportElement x="30" y="0" width="150" height="15"/>
                <textFieldExpression><![CDATA[$F{rental_date}]]></textFieldExpression>
            </textField>
            <textField isBlankWhenNull="true">
                <reportElement x="190" y="0" width="260" height="15"/>
                <textFieldExpression><![CDATA[$F{title} == null ? "Sense lloguers" : $F{title}]]></textFieldExpression>
            </textField>
        </band>
    </detail>
</jasperReport>
```

**Consell per a l'alumne:** Si l'informe genera milers de pàgines (Sakila té molts lloguers), recomana'ls afegir un `LIMIT 100` a la consulta SQL mentre estiguin fent proves de disseny.