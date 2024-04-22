# Instalacion de Odoo mediante Docker

![1](https://github.com/FranciscoFerreiraT/Odoo_Instalaci-n/assets/92456485/1029ae95-3ff7-44f8-871b-46236be7f50d)

## Explicación de Docker-compose

  
    version: '3.1'

Indica la versión del  docker-compose

    services:
    
Ahora se definen los servicios

      web:
    image: odoo:16.0

Define un servicio llamado web que utiliza la imagen de Docker odoo:16.0.

        depends_on:
      - db
      
 Indica que este servicio (web) depende del servicio llamado db. 

         ports:
      - "8069:8069"


  Mapea los puertos entre el host y el contenedor. En este caso, el puerto 8069 del host se mapea al puerto 8069 del contenedor.

          volumes:
      - odoo_data:/var/lib/odoo
      
Define un volumen llamado odoo_data que se utilizará para persistir los datos en el directorio /var/lib/odoo dentro del contenedor.

      db:
    image: postgres:15

Define un servicio llamado db que utiliza la imagen de Docker postgres:15

        environment:
      - POSTGRES_DB=postgres
      - POSTGRES_PASSWORD=odoo
      - POSTGRES_USER=odoo

Establece las variables de entorno necesarias para la base de datos PostgreSQL, como el nombre de la base de datos (POSTGRES_DB), la contraseña del usuario (POSTGRES_PASSWORD), y el nombre de usuario (POSTGRES_USER).

        volumes:
      - postgres_data:/var/lib/postgresql/data

Define un volumen llamado postgres_data que se utilizará para persistir los datos en el directorio /var/lib/postgresql/data dentro del contenedor de la base de datos.

      volumes:
    odoo_data:
    postgres_data:

Define volúmenes externos (odoo_data y postgres_data). 


## Una vez se ejecute el docker compose vamos a nuestro localhost


![2](https://github.com/FranciscoFerreiraT/Odoo_Instalaci-n/assets/92456485/ad246a7d-dc6f-4c23-b77c-d2c431b9b8a4)

El odoo ya estaria listo



## Puerto ocupado

Si el puerto esta ocupado al hacer el docker-compose up da el siguiente error

    ERROR: for db  Cannot start service db: driver failed programming external connectivity on endpoint your_project_db_1

Para solucionar se debe cambiar el mapeo de puertos en el docker-compose

    ports:
    - "5433:5432"

