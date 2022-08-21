# Comandos docker

## Imagenes

Muestra las imagenes instaladas

    docker images

Descargar imagenes

    docker pull <Nombre imagen ej: node>:<opcional podemos espesificar la version>

Eliminar imagenes

    docker image rm <imagen>:<version>

---

## Contenedores

Crear un contenedor

    docker create <Nombre imagen> | docker container create <Nombre imagen>

Iniciar contenedor

    docker start <ID> | docker start <nombre>

Ver contenedores corriendo

    docker ps

Parar contenedor

    docker stop <ID>

Mostrar todos los contenedores

    docker ps -a

Eliminar contenedor

    docker rm <nombre del contenedor>

Crear y asignar nombre

    docker create --name <Nombre a escoger> <nombre imagen>

Crear y asignar puertos

    docker create -p<puerto maquina>:<puerto de salida> --name <Nombre> <nombre imagen>
    <ej: docker create -p27017:2707 --name monguito mongo>

Ver logs

    docker logs <nombre> | docker --folow <nombre>

---

## Recopilacion de todo

El siguiente comando ejecuta docker pull, docker create y docker logs en uno solo

    docker run <imagen>

Para no ver los logs usamos

    docker run -d <imagen>

A docker run se le puede aplicar todo los argumentos previamente vistos

---

## Aplicando lo anterior

    docker pull mongo
    docker create -p27017:27017 --name monguito -e MONGO_INITDB_ROOT_USERNAME=admin -e MONGO_INITDB_ROOT_PASSWORD=1234 mongo
    docker start monguito
    docker ps

---

## Contenedores que se comunican entre si

Ver redes de docker

    docker network ls

Crear red

    docker network create <nombre de la red ej: mired>

Eliminar red

    docker network rm <nombre ej: mired>

PD: en la aplicacion a crear en la ruta de conexion e: mongo cambiamos localhost por el nombre del contenedor

Ej:

    mongoose.connect('mongodb://admin:1234@monguito:27017/miapp?authSource=admin')

para espesificar la red en los contenedores hacemos lo sig:

    docker create -p2707:2707 --name monguito --network mired -e MONGO_INITDB_ROOT_USERNAME=admin -e MONGO_INITDB_ROOT_PASSWORD=1234 mongo

    docker create -p3000:3000 --name node --network mired node

---

## Ahorrando todo lo anterior xd

Creamos un archivo llamado docker-comose.yml con todo lo que ocuparemos

Ej:

[Archivo SOLO de ejemplo](https://github.com/MrPotatoXx/curso-docker/blob/main/docker-compose.yml)

luego en la terminal ejecutamos

    docker compose up

Eliminar todo lo creado con docker compose

    docker compose down

---

## Volumenes para persistir los archivos

Estan al final de: 

- [Archivo SOLO de ejemplo](https://github.com/MrPotatoXx/curso-docker/blob/main/docker-compose.yml)