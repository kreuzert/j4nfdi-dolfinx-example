FROM quay.io/jupyter/base-notebook:notebook-7.4.3

# Install required system packages using apt (base-notebook is Debian-based)
USER root
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Switch back to the default user
USER ${NB_UID}

# Copy conda environment and install it
COPY binder/environment.yml /tmp/environment.yml

RUN mamba env create -f /tmp/environment.yml && \
    conda clean --all -f -y && \
    echo "conda activate fenicsx-env" >> ~/.bashrc

# Set default environment
ENV CONDA_DEFAULT_ENV=fenicsx-env
ENV PATH=/opt/conda/envs/fenicsx-env/bin:$PATH
