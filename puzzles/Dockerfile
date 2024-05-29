# Stage 1: Build environment
FROM python:3.12-slim-bookworm

# Set working directory
WORKDIR /app

# Install system dependencies (if needed)
RUN apt-get update && apt-get install -y --no-install-recommends \
    git \
    wget \
    vim \
    curl \
    bzip2 \
    ca-certificates \
    libglib2.0-0 \
    libxext6 \
    libsm6 \
    libxrender1 \
    mercurial \
    subversion \
    gcc \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Copy requirements file
COPY requirements.txt .

# Create a virtual environment
RUN python -m venv venv

# Activate the virtual environment
ENV PATH="/app/venv/bin:$PATH"

# Install data science dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Create a non-root user named 'jovyan'
RUN useradd -m -s /bin/bash nopriv

# Expose port 8888
EXPOSE 8888

#Add unpriviledged user for juypter
USER nopriv 

# Start Jupyter Notebook
CMD ["jupyter", "notebook", "--port", "8888", "--ip", "0.0.0.0", "--no-browser"]
