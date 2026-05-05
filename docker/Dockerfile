# Base Python image (lightweight)
FROM python:3.11-slim

# Container working directory
WORKDIR /app

# Environment settings
# Don't create __pycache__ files (keeps repo clean)
# Don't store pip download cache (smaller image)
# Make hashing deterministic (reproducible runs)
# Set timezone to UTC (consistent timestamps/logs)
# Ensure consistent UTF-8 locale handling
# Avoid encoding issues when reading files
# Disable pip update warnings
# Tell Python to look in /app for packages
ENV PYTHONDONTWRITEBYTECODE=1 \
    PIP_NO_CACHE_DIR=1 \
    PYTHONHASHSEED=0 \
    TZ=UTC \
    LC_ALL=C.UTF-8 \
    LANG=C.UTF-8 \
    PIP_DISABLE_PIP_VERSION_CHECK=1 \
    PYTHONPATH=/app

# Install system build tools needed for packages like scikit-surprise
RUN apt-get update && \
    apt-get install -y --no-install-recommends build-essential && \
    rm -rf /var/lib/apt/lists/*

# Analysis only project, no source is copied. Just install dependencies.
# Install dependencies by making a copy requirements.txt in the container
COPY requirements.txt /tmp/requirements.txt
RUN pip install --no-cache-dir -r /tmp/requirements.txt


# Expose a port (used by Jupyter or your API if needed)
EXPOSE 8888


# Default command for dev: keep container alive and interactive
CMD ["jupyter", "lab", "--ip=0.0.0.0", "--no-browser", "--allow-root", "--ServerApp.token="]

