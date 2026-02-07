# Use the official CUDA base image
FROM nvidia/cuda:12.9.1-cudnn-runtime-ubuntu24.04

# Install system dependencies (with fish)
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    build-essential \
    ca-certificates \
    curl \
    fish \
    git \
    libffi-dev \
    libssl-dev \
    sudo \
    && \
    rm -rf /var/lib/apt/lists/*

# Set up a non-root user for development
RUN useradd -m -s /usr/bin/fish devuser && \
    echo "devuser ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

# Switch to non-root user
USER devuser
WORKDIR /workspace

# Update PATH to include uv
ENV PATH="/home/devuser/.local/bin:/home/devuser/.cargo/bin:$PATH"

# Install UV, Python 3.10, and create venv
RUN curl -LsSf https://astral.sh/uv/install.sh | sh && \
    uv python install 3.10 && \
    uv venv ~/.venv --python 3.10

# Activate the virtual environment in the environment variables
ENV VIRTUAL_ENV="/home/devuser/.venv"
ENV PATH="$VIRTUAL_ENV/bin:$PATH"
ENV PYTHONPATH=/workspace

# Default command
CMD ["fish"]
