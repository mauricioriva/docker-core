# Imagen base mínima basada en Alpine Linux
FROM alpine:latest

# -------------------------------
# Instalar Node.js y npm
# También instalamos herramientas necesarias para compilar dependencias nativas
# -------------------------------
RUN apk add --no-cache nodejs npm python3 make g++ git

# -------------------------------
# Establecer directorio de trabajo
# -------------------------------
WORKDIR /app

# -------------------------------
# Copiar los archivos de dependencias primero
# Esto permite aprovechar la cache de Docker si package.json no cambia
# -------------------------------
COPY package*.json ./

# -------------------------------
# Instalar solo dependencias de producción
# --omit=dev evita instalar dependencias de desarrollo
# -------------------------------
RUN npm install --omit=dev

# -------------------------------
# Copiar el resto del código fuente
# -------------------------------
COPY . .

# -------------------------------
# Exponer el puerto usado por la app (NestJS = 3000)
# -------------------------------
EXPOSE 3000

# -------------------------------
# Comando por defecto para ejecutar la aplicación
# -------------------------------
CMD ["npm", "run", "start"]
