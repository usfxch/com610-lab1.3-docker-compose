# Laboratorio 1.3: Orquestación de Contenedores con Docker Compose

Este laboratorio introduce los conceptos básicos de orquestación de contenedores utilizando Docker Compose como herramienta principal. Docker Compose es una herramienta poderosa para definir y gestionar aplicaciones multi-contenedor. Aquí tienes varios ejemplos de uso, desde los más básicos hasta escenarios un poco más complejos:

## Ejemplo 1: Aplicación Web Simple con un Contenedor (Nginx)

Este es el caso más sencillo, donde solo tienes un servicio web.

**`docker-compose.yml`:**

```yaml
version: '3.1'
services:
  web:
    image: nginx:latest
    ports:
      - "80:80"
    volumes:
      - ./html:/usr/share/nginx/html:ro
```

**Explicación:**

  * `version: '3.1'`: Especifica la versión del formato del archivo Docker Compose.
  * `services:`: Define los servicios que componen la aplicación.
  * `web:`: Define un servicio llamado `web`.
      * `image: nginx:latest`: Utiliza la última imagen oficial de Nginx desde Docker Hub.
      * `ports: - "80:80"`: Mapea el puerto 80 del contenedor al puerto 80 de la máquina host.
      * `volumes: - ./html:/usr/share/nginx/html:ro`: Monta un directorio local `./html` en el directorio `/usr/share/nginx/html` dentro del contenedor (donde Nginx sirve los archivos web). `:ro` indica que el montaje es de solo lectura desde el contenedor.

**Uso:**

1.  Crea un directorio llamado `html` en el mismo lugar que tu `docker-compose.yml`.
2.  Dentro de `html`, crea un archivo `index.html` con algún contenido.
3.  Ejecuta `bash docker-compose up -d` en el directorio donde está `docker-compose.yml`.
4.  Abre tu navegador y ve a `http://localhost`. Deberías ver el contenido de tu `index.html`.
5.  Para detener y eliminar los contenedores, ejecuta `bash docker-compose down`