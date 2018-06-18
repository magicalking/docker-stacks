# Start with the a minmal jupyter notebook
FROM jupyter/minimal-notebook

# Activate the 'root' user
USER root

RUN wget -O - https://apt.llvm.org/llvm-snapshot.gpg.key | sudo apt-key add - \
 && apt-add-repository "deb http://apt.llvm.org/xenial/ llvm-toolchain-xenial-6.0 main" \
 && apt-get update && apt-get install -yq --no-install-recommends \
    clang-6.0 \
    gcc \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*

RUN update-alternatives --install /usr/bin/clang++ clang++ /usr/bin/clang++-3.8 100 \
 && update-alternatives --install /usr/bin/clang++ clang++ /usr/bin/clang++-6.0 1000 \
 && update-alternatives --install /usr/bin/clang++ clang /usr/bin/clang-3.8 100 \
 && update-alternatives --install /usr/bin/clang clang /usr/bin/clang-3.8 100 \
 && update-alternatives --install /usr/bin/clang clang /usr/bin/clang-6.0 1000 \
 && update-alternatives --config clang \
 && update-alternatives --config clang++

# Activate the 'joyvan' user
USER $NB_UID

# Install xeus-calling
RUN conda install --quiet --yes \
    -c QuantStack \
    -c conda-forge \
    xeus-cling && \
    conda clean -tipsy && \
    fix-permissions $CONDA_DIR
