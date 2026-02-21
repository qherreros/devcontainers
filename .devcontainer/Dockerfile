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
    openssh-client \
    sudo \
    && \
    rm -rf /var/lib/apt/lists/*

# Set up a non-root user for development
ARG USERNAME=ubuntu

# Switch to non-root user
USER $USERNAME

# Pre-create fish history directory so the named volume is initialized
# with the correct ownership (created as ubuntu, not root)
RUN mkdir -p /home/$USERNAME/.local/share/fish
WORKDIR /workspace

# Update PATH to include uv
ENV PATH="/home/$USERNAME/.local/bin:/home/$USERNAME/.cargo/bin:$PATH"

# Install UV, Python 3.10, and create venv
RUN curl -LsSf https://astral.sh/uv/install.sh | sh && \
    uv python install 3.10 && \
    uv venv --python 3.10

# Default command and activate venv in fish
CMD ["fish"]
