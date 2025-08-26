FROM alpine:3.20

# Instalar dependencias del sistema + Python
RUN apk add --no-cache \
    python3 \
    py3-pip \
    curl \
    bash \
    gcc \
    musl-dev \
    libffi-dev \
    python3-dev

# Asegurar que "python" apunte a python3
RUN ln -sf python3 /usr/bin/python

# Instalar uv
RUN curl -LsSf https://astral.sh/uv/install.sh | sh \
    && mv /root/.local/bin/uv /usr/local/bin/uv

WORKDIR /app

# Copiar dependencias primero (cache)
COPY pyproject.toml uv.lock* ./
RUN uv sync --frozen

# Copiar código
COPY . .

CMD ["uv", "run", "python", "main.py"]
