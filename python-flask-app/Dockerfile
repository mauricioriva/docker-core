FROM alpine

# Set environment variables
ENV PYTHONUNBUFFERED=1 \
    PYTHONDONTWRITEBYTECODE=1

# Install Python and curl
RUN apk add --no-cache \
    python3 \
    py3-pip \
    curl

# Download and install uv (static binary)
RUN curl -LsSf https://astral.sh/uv/install.sh | sh

# Add uv to PATH
ENV PATH="/root/.local/bin:$PATH"

# Set work directory
WORKDIR /app

# Copy application files
COPY . .

# Expose Flask port
EXPOSE 3000

# Use uv to run the app
CMD ["uv", "run", "main.py"]
