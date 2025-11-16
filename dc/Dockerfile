FROM python:3.12-slim

# ---- System setup ----
RUN apt-get update && \
    apt-get install -y curl && \
    rm -rf /var/lib/apt/lists/*

# Install uv (required by dremio-mcp)
RUN pip3 install --no-cache-dir uv

# Non-root user (security best practice)
RUN useradd -m appuser
WORKDIR /app
USER appuser

# ---- Install Dremio MCP Server ----
# Option 1: install from PyPI (preferred if available)
# RUN pip install --no-cache-dir dremio-mcp

# Option 2: install from GitHub (most common today)
RUN pip3 install --no-cache-dir \
    git+https://github.com/dremio/dremio-mcp.git

# ---- Runtime ----
EXPOSE 3333

ENTRYPOINT ["dremio-mcp-server", "run"]

