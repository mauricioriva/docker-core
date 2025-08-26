# Proyecto Fullstack: NestJS + Flask

Este proyecto contiene dos aplicaciones:
1. **NestJS** (Node.js) corriendo en `nestjs-app`.
2. **Flask** (Python) corriendo en `flask-app`.

Ambas aplicaciones pueden ejecutarse en contenedores Docker, ya sea **juntas** con Docker Compose o **por separado** con `docker run`.

---

## Requisitos

- [Docker](https://www.docker.com/get-started)
- [Docker Compose](https://docs.docker.com/compose/install/)

---

## Levantar con Docker Compose

1. Desde la raíz del proyecto, ejecuta:

```bash
docker-compose up --build
````

2. Esto hará lo siguiente:

   * Construirá las imágenes de `nestjs-app` y `flask-app`.
   * Levantará ambos contenedores.
   * Mapeará los puertos:

     * NestJS → `localhost:3001`
     * Flask → `localhost:3000`

3. Para detener los contenedores:

```bash
docker-compose down
```

---

## Levantar cada contenedor por separado con `docker run`

### 1. NestJS

1. Construir la imagen:

```bash
docker build -t nestjs-app ./node-nestjs-app
```

2. Ejecutar el contenedor:

```bash
docker run -d \
  --name nestjs-app \
  -p 3001:3000 \
  -e NODE_ENV=development \
  nestjs-app
```

---

### 2. Flask

1. Construir la imagen:

```bash
docker build -t flask-app ./python-flask-app
```

2. Ejecutar el contenedor:

```bash
docker run -d \
  --name flask-app \
  -p 3000:3000 \
  -e FLASK_ENV=development \
  flask-app
```

---

## Notas

* Flask corre en el puerto **3000** y NestJS en **3001** (puedes cambiar los puertos en `docker-compose.yml` o con `-p` en `docker run`).
* Se recomienda usar Docker Compose para levantar ambos contenedores juntos, ya que maneja automáticamente dependencias y orden de arranque.
* Para desarrollo, los contenedores están configurados con variables de entorno `development`.

---

## Recursos útiles

* [Documentación NestJS](https://docs.nestjs.com/)
* [Documentación Flask](https://flask.palletsprojects.com/)
* [Documentación Docker](https://docs.docker.com/)
