<div class="logo-container"><img src="https://xsastre.github.io/imatges/logosxs/DESINT.png" alt="Logo esquerra" class="header-image"></div>

# Desenvolupament d'interfícies - Codi Exercicis Mòdul DESINT

![Java](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)
![JasperReports](https://img.shields.io/badge/JasperReports-2C3E50?style=for-the-badge&logo=jasperreports&logoColor=white)
![MariaDB](https://img.shields.io/badge/MariaDB-003545?style=for-the-badge&logo=mariadb&logoColor=white)
![VS Code](https://img.shields.io/badge/VS%20Code-007ACC?style=for-the-badge&logo=visual-studio-code&logoColor=white)
![Maven](https://img.shields.io/badge/Apache%20Maven-C71A36?style=for-the-badge&logo=apache-maven&logoColor=white)
[![Accessos al repo](https://img.shields.io/github/views/xsastre/md_pages?label=Accessos&style=or-the-badge)](https://github.com/xsastre/md_pages/graphs/traffic)
[![Clons del repo](https://img.shields.io/github/clones/xsastre/md_pages?label=Clons&style=or-the-badge)](https://github.com/xsastre/md_pages/graphs/traffic)

Recopilació de codis i exercicis del mòdul de Desenvolupament d'Interfícies (DESINT) del cicle de DAM.

## Continguts

### JasperReports (JasperSoft Studio)

Aquest repositori conté diversos exercicis i exemples d'ús de JasperReports per a la generació d'informes.

#### Enunciats
- [Col·lecció completa d'exercicis per Jasper Studio](./Col%C2%B7lecci%C3%B3%20exercicis%20per%20Jasper%20Studio.md)

#### Solucions
- Dins la carpeta `Solucions_Jasper` es poden trobar solucions, indicacions i codi a diversos exercicis. També nclou un `docker-compose.yml` per aixecar entorns de proves. (seguint .devcontainer)


## Entorn de Desenvolupament (Dev Container)
Aquest repositori inclou una configuració de **Dev Container** per a VS Code que munta automàticament:
- Un entorn **Java 17** amb Maven.
- Una base de dades **MariaDB** amb la base de dades de proves **Sakila** ja carregada.

### Com utilitzar-lo:
1. Obre el projecte amb VS Code.
2. Si tens instal·lada l'extensió "Dev Containers", t'apareixerà un missatge per "Reopen in Container".
3. VS Code baixarà les imatges i configurarà la base de dades automàticament.
4. **Dades de connexió a la BD**:
   - **Host**: `db` (o `localhost` si connectes des de fora del contenidor pel port 3306)
   - **User**: `root`
   - **Password**: `root`
   - **Database**: `sakila`
