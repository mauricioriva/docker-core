
# https://hub.docker.com/_/alpine
FROM alpine

FROM alpine:3.20

# Instalar Node.js + npm
RUN apk add --no-cache nodejs npm \
    && apk add --no-cache python3 make g++ git

# Crear directorio de la app
WORKDIR /app

# Copiar primero los manifests para instalar dependencias
COPY package*.json ./

# Instalar dependencias (produce node_modules)
RUN npm install --omit=dev

# Copiar el resto del código
COPY . .

# Exponer puerto (NestJS usa 3000 por default)
EXPOSE 3000

# Arrancar con npm run start
CMD ["npm", "run", "start"]
