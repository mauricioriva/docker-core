# Proyecto Fullstack: NestJS + Flask

Este proyecto contiene dos aplicaciones:

1. **NestJS** (Node.js) corriendo en `nestjs-app`.
2. **Flask** (Python) corriendo en `flask-app`.

Ambas aplicaciones pueden ejecutarse en contenedores Docker, ya sea **juntas** con Docker Compose o **por separado** con `docker run`.

---

## Requisitos

* [Docker](https://www.docker.com/get-started)
* [Docker Compose](https://docs.docker.com/compose/install/)
* [GitHub Actions](https://docs.github.com/en/actions) (para CI/CD)

---

## Levantar con Docker Compose

1. Desde la raíz del proyecto, ejecuta:

```bash
docker-compose up --build
```

2. Esto hará lo siguiente:

   * Construirá las imágenes de `nestjs-app` y `flask-app`.
   * Levantará ambos contenedores.
   * Mapeará los puertos:

     * **NestJS** → `localhost:3001`
     * **Flask** → `localhost:3000`

3. Para detener los contenedores:

```bash
docker-compose down
```

---

## Levantar cada contenedor por separado con `docker run`

### **1. NestJS**

**Construir la imagen:**

```bash
docker build -t nestjs-app ./node-nestjs-app
```

**Ejecutar el contenedor:**

```bash
docker run -d \
  --name nestjs-app \
  -p 3001:3000 \
  -e NODE_ENV=development \
  nestjs-app
```

---

### **2. Flask**

**Construir la imagen:**

```bash
docker build -t flask-app ./python-flask-app
```

**Ejecutar el contenedor:**

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

## CI con GitHub Actions

Este proyecto incluye **workflows de GitHub Actions** para **construir y subir imágenes Docker a Docker Hub**.

### 📂 **Workflows definidos**

En la carpeta `.github/workflows/` hay los siguientes archivos:

* **`docker-build-dev.yml`** → Ejecuta en **push a la rama `dev`**.
* **`docker-build-staging.yml`** → Ejecuta en **push a la rama `staging`**.
* **`docker-build-prod.yml`** → Ejecuta en **push a la rama `prod`**.
* **`docker-build-pr.yml`** → Ejecuta en **Pull Requests** hacia `dev`, `staging` o `prod` (solo build, no push).

---

### ¿Cómo se disparan los pipelines?

| **Acción**                            | **Workflow que se ejecuta** | **Qué hace**                                |
| ------------------------------------- | --------------------------- | ------------------------------------------- |
| Push en `dev`                         | `docker-build-dev.yml`      | Construye y sube imágenes con tag `dev`     |
| Push en `staging`                     | `docker-build-staging.yml`  | Construye y sube imágenes con tag `staging` |
| Push en `prod`                        | `docker-build-prod.yml`     | Construye y sube imágenes con tag `latest`  |
| Pull Request hacia `dev/staging/prod` | `docker-build-pr.yml`       | Construye imágenes **sin subir**            |

---

### Tags generados en Docker Hub

* Rama **dev** → `nestjs-app:dev` y `flask-app:dev`
* Rama **staging** → `nestjs-app:staging` y `flask-app:staging`
* Rama **prod** → `nestjs-app:latest` y `flask-app:latest`

---

### Variables de entorno requeridas en GitHub

Agrega en **Settings → Secrets → Actions**:

* `DOCKERHUB_USERNAME` → tu usuario de Docker Hub
* `DOCKERHUB_TOKEN` → token de acceso de Docker Hub

---

## Recursos útiles

* [Documentación NestJS](https://docs.nestjs.com/)
* [Documentación Flask](https://flask.palletsprojects.com/)
* [Documentación Docker](https://docs.docker.com/)
* [Documentación GitHub Actions](https://docs.github.com/en/actions)
