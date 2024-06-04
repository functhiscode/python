# Stage 1: Build environment
FROM tensorflow/tensorflow:latest-gpu-jupyter

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
    libgl1-mesa-glx \
    libglib2.0-0 \
    libxext6 \
    libsm6 \
    libxrender1 \
    mercurial \
    subversion \
    gcc \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

#Install Juypter Notebook extensions
RUN pip install jupyterlab-myst jupyter_contrib_nbextensions notebook jupyterlab

# Copy requirements file
COPY requirements.txt .

# Create a virtual environment
RUN python -m venv venv

# Activate the virtual environment
ENV PATH="/app/venv/bin:$PATH"

# Install data science dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Append the desired path to sys.path
ENV PYTHONPATH="/app/venv/lib/python3.11/site-packages:$PYTHONPATH"

# Create a non-root user named 'nopriv'
#RUN useradd -m -s /bin/bash nopriv

# Create /tf/notebooks and add ownership to nopriv user
#RUN mkdir -p /tf/notebooks && chown -R nopriv:nopriv /tf && chown -R nopriv:nopriv /app

# Expose port 8888
EXPOSE 8888

#Add unpriviledged user for juypter
#USER nopriv 

# Start Jupyter Notebook
CMD ["jupyter", "notebook", "--notebook-dir", "/tf", "--ip", "0.0.0.0", "--port", "8888", "--no-browser","--allow-root", "--NotebookApp.allow_origin", "'https://colab.research.google.com'"]

