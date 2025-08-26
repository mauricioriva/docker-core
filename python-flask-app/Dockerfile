# Imagen base mínima basada en Alpine Linux
FROM alpine:latest

# -------------------------------
# Variables de entorno para optimizar Python:
# - PYTHONUNBUFFERED=1 -> Salida sin buffer (logs en tiempo real)
# - PYTHONDONTWRITEBYTECODE=1 -> Evita generar archivos .pyc
# -------------------------------
ENV PYTHONUNBUFFERED=1 \
    PYTHONDONTWRITEBYTECODE=1

# -------------------------------
# Instalar Python, pip y curl
# -------------------------------
RUN apk add --no-cache python3 py3-pip curl

# -------------------------------
# Instalar uv (binario estático para manejar entornos y dependencias)
# -------------------------------
RUN curl -LsSf https://astral.sh/uv/install.sh | sh

# -------------------------------
# Agregar uv al PATH (instalado en ~/.local/bin)
# -------------------------------
ENV PATH="/root/.local/bin:$PATH"

# -------------------------------
# Establecer directorio de trabajo
# -------------------------------
WORKDIR /app

# -------------------------------
# Copiar el código fuente de la aplicación
# -------------------------------
COPY . .

# -------------------------------
# Exponer el puerto usado por Flask (por defecto 3000 en este caso)
# -------------------------------
EXPOSE 3000

# -------------------------------
# Comando por defecto: ejecutar la app usando uv
# -------------------------------
CMD ["uv", "run", "main.py"]
