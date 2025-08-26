# https://hub.docker.com/_/alpine
FROM alpine:3.20

# Instalar Node.js y npm
RUN apk add --no-cache nodejs npm

# Crear directorio de la app
WORKDIR /app

# Copiar package.json y package-lock.json primero (para aprovechar cache)
COPY package*.json ./

# Instalar dependencias
RUN npm install

# Copiar el resto del código
COPY . .

# Construir el proyecto (Nest usa TypeScript → compila a JS)
RUN npm run build

# Exponer el puerto (por defecto Nest usa 3000)
EXPOSE 3000

# Ejecutar el servidor (ejecuta el JS compilado)
# Ejecutar el servidor (ejecuta el JS compilado)
CMD ["node", "dist/main.js"]
