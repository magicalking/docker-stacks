# Start with the a minmal jupyter notebook
FROM jupyter/minimal-notebook

# Activate the 'root' user
USER root

# C++ pre-requisites
RUN apt-get update && \
    apt-get install -y --no-install-recommends gcc && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Activate the 'joyvan' user
USER $NB_UID

# Install xeus-calling
RUN conda install --quiet --yes \
    -c QuantStack \
    -c conda-forge \
    xeus-cling && \
    conda clean -tipsy && \
    fix-permissions $CONDA_DIR
