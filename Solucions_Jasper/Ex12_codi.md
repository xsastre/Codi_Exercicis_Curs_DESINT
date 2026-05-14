```java GeneradorInformes.java
package docencia.xaviersastre.dam.di;  
  
import net.sf.jasperreports.engine.*;  
import net.sf.jasperreports.engine.util.JRLoader;  
import java.sql.Connection;  
import java.sql.DriverManager;  
import java.sql.SQLException;  
import java.util.HashMap;  
import java.util.Map;  
  
public class GeneradorInforme {  
  
    public static void main(String[] args) {  
        // 1. Paràmetres de connexió a la base de dades (Docker MariaDB)  
        String url = "jdbc:mariadb://localhost:3306/sakila";  
        String usuari = "student";  
        String password = "password123";  
  
        // 2. Rutes dels fitxers  
        String fitxerEntrada = "src/main/resources/Ex11_sakila.jrxml";  
        String fitxerSortida = "Informe_Sakila_Socis.pdf";  
  
        Connection conn = null;  
  
        try {  
            System.out.println("Connectant a la base de dades...");  
            conn = DriverManager.getConnection(url, usuari, password);  
  
            System.out.println("Compilant l'informe...");  
            // Compila el fitxer .jrxml per generar un fitxer executable .jasper en memòria  
            JasperReport report = JasperCompileManager.compileReport(fitxerEntrada);  
  
            // 3. Paràmetres de l'informe (en aquest cas buit, però necessari per la  
            // signatura del mètode)            Map<String, Object> parameters = new HashMap<>();  
  
            System.out.println("Omplint l'informe amb dades...");  
            // Omple l'informe amb la connexió SQL i els paràmetres  
            JasperPrint jasperPrint = JasperFillManager.fillReport(report, parameters, conn);  
  
            System.out.println("Generant el PDF...");  
            // Exporta l'objecte JasperPrint a un fitxer PDF físic  
            JasperExportManager.exportReportToPdfFile(jasperPrint, fitxerSortida);  
  
            System.out.println("Èxit! L'informe s'ha generat correctament a: " + fitxerSortida);  
  
        } catch (JRException e) {  
            System.err.println("Error de JasperReports: " + e.getMessage());  
            e.printStackTrace();  
        } catch (SQLException e) {  
            System.err.println("Error de connexió SQL: " + e.getMessage());  
            e.printStackTrace();  
        } finally {  
            // Tancar la connexió sempre  
            try {  
                if (conn != null && !conn.isClosed()) {  
                    conn.close();  
                }  
            } catch (SQLException e) {  
                e.printStackTrace();  
            }  
        }  
    }  
}
``` 

```xml pom.xml
<?xml version="1.0" encoding="UTF-8"?>  
<project xmlns="http://maven.apache.org/POM/4.0.0"  
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">  
    <modelVersion>4.0.0</modelVersion>  
  
    <groupId>docencia.xaviersastre.dam.di</groupId>  
    <artifactId>DESINTInformes_sakila</artifactId>  
    <version>1.0-SNAPSHOT</version>  
  
    <properties>  
        <maven.compiler.source>23</maven.compiler.source>  
        <maven.compiler.target>23</maven.compiler.target>  
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>  
    </properties>  
    <dependencies>  
        <dependency>  
            <groupId>net.sf.jasperreports</groupId>  
            <artifactId>jasperreports</artifactId>  
            <version>6.20.0</version>  
        </dependency>  
  
        <dependency>  
            <groupId>org.mariadb.jdbc</groupId>  
            <artifactId>mariadb-java-client</artifactId>  
            <version>3.1.2</version>  
        </dependency>  
  
        <dependency>  
            <groupId>org.apache.commons</groupId>  
            <artifactId>commons-collections4</artifactId>  
            <version>4.4</version>  
        </dependency>  
  
        <dependency>  
            <groupId>org.slf4j</groupId>  
            <artifactId>slf4j-simple</artifactId>  
            <version>2.0.5</version>  
        </dependency>  
    </dependencies></project>
```