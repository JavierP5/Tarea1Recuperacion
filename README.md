# Tarea1Recuperacion  

# TAREA 1 - Recuperación: Instalación de Odoo 17 Community y PgAdmin con Docker Compose  


## Objetivo  

El objetivo de esta tarea es instalar **Odoo 17 Community Edition** y **PgAdmin** utilizando **Docker Compose**. Se deben seguir los pasos detallados   para configurar los contenedores de **PostgreSQL**, **Odoo** y **PgAdmin**, y resolver posibles conflictos de puertos ocupados.  


## Requisitos  

- **Docker** y **Docker Compose** deben estar instalados en tu máquina local.  
- **PgAdmin** debe estar configurado para conectarse a la base de datos de Odoo.  


## Configuración del Docker Compose  

El archivo `docker-compose.yml` es el encargado de definir los contenedores necesarios para **PostgreSQL**, **Odoo** y **PgAdmin**. A continuación se   muestra el contenido del archivo:  



services:  
  db:  
    image: postgres:15  
    container_name: odoo-db  
    environment:  
      - POSTGRES_DB=postgres  
      - POSTGRES_USER=putin  
      - POSTGRES_PASSWORD=putin  
    ports:  
      - "5433:5432"  # Cambiado el puerto para evitar conflicto  
    volumes:  
      - odoo-db-data:/var/lib/postgresql/data  

  odoo:  
    image: odoo:17  
    container_name: odoo  
    depends_on:  
      - db  
    ports:  
      - "8070:8069"  # Cambiado el puerto para evitar conflicto  
    environment:  
      - HOST=db  
      - USER=putin  
      - PASSWORD=putin  
    volumes:  
      - odoo-web-data:/var/lib/odoo  
      - ./addons:/mnt/extra-addons  

  pgadmin:  
    image: dpage/pgadmin4  
    container_name: pgadmin  
    environment:  
      - PGADMIN_DEFAULT_EMAIL=admin@admin.com  
      - PGADMIN_DEFAULT_PASSWORD=putin  
    ports:  
      - "5050:80"  

volumes:  
  odoo-db-data:  
  odoo-web-data:  


### Explicación del archivo `docker-compose.yml`:  

- **db**: Configura el contenedor de **PostgreSQL**. Se usa el puerto `5433:5432` para evitar conflictos con otros servicios que puedan estar usando el   puerto 5432.    
- **odoo**: Configura el contenedor de **Odoo 17**. El puerto se cambia a `8070:8069` para evitar conflictos con otros servicios que puedan estar usando el puerto 8069.  
- **pgadmin**: Configura el contenedor de **PgAdmin** con los puertos `5050:80`, para acceder al panel de administración de la base de datos desde el navegador.  


## Instrucciones de Uso  

1. **Clonar el Repositorio**:  

git clone <url-del-repositorio>  
cd <nombre-del-repositorio>  
  

2. **Levantar los Contenedores**:  

Ejecuta el siguiente comando para levantar los contenedores de Docker:  
  

docker-compose up -d  


3. **Acceder a los Servicios**:  

- **Odoo**: Accede a Odoo en [http://localhost:8070](http://localhost:8070).  
- **PgAdmin**: Accede a PgAdmin en [http://localhost:5050](http://localhost:5050).  


## Credenciales  

### PgAdmin:  

- **Email**: admin@admin.com  
- **Contraseña**: admin  

### Base de Datos PostgreSQL:  

- **Usuario**: odoo  
- **Contraseña**: odoo  
- **Host**: db  
- **Puerto**:  5433 (modificado para evitar conflicto con otro servicio)  



## Resolución de Conflictos de Puertos  

### Si el puerto **5432** (PostgreSQL) está ocupado:  

Si el puerto 5432 está siendo utilizado por otro servicio en tu máquina, puedes cambiar el puerto local de PostgreSQL en el archivo `docker-  compose.yml`, como se muestra a continuación:  


ports:  
  - "5433:5432"  # Cambié el puerto 5432 a 5433  


### Si el puerto **8069** (Odoo) está ocupado:  

De igual manera, si el puerto 8069 está ocupado, puedes cambiar el puerto local de Odoo en el archivo `docker-compose.yml`:  


ports:  
  - "8070:8069"  # Cambié el puerto 8069 a 8070  




## Capturas de Pantalla  

A continuación se muestran las capturas de pantalla que demuestran que **Odoo** y **PgAdmin** se han instalado y configurado correctamente.  

### Odoo funcionando:

![Odoo Home]

### Módulo instalado en Odoo:

![Módulo en Odoo]

### Conexión a la base de datos en PgAdmin:

![PgAdmin Conectado]()




