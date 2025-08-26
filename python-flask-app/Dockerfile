FROM alpine:3.20

# Instalar Python y dependencias básicas
RUN apk add --no-cache python3 py3-pip curl build-base

# Instalar uv
RUN curl -LsSf https://astral.sh/uv/install.sh | sh -s -- --yes \
 && mv /root/.local/bin/uv /usr/local/bin/uv

# Directorio de la app
WORKDIR /app

# Copiar archivos del proyecto
COPY pyproject.toml .
COPY main.py .

# Crear entorno con uv
RUN uv sync

# Comando por defecto -> usar uv para correr la app
CMD ["uv", "run", "python", "main.py"]
