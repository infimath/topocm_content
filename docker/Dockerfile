# Adopted from jupyter/docker-stacks Dockerfile's
# Copyright (c) 2016 Jupyter Development Team.
# Distributed under the terms of the Modified BSD License.

FROM debian@sha256:32a225e412babcd54c0ea777846183c61003d125278882873fb2bc97f9057c51

MAINTAINER Anton Akhmerov <anton.akhmerov@gmail.com>

USER root

RUN apt-get update && apt-get install -yq --no-install-recommends \
    dvipng \
    git \
    build-essential \
    python-dev \
    unzip \
    libsm6 \
    pandoc \
    texlive-latex-base \
    texlive-latex-extra \
    texlive-fonts-extra \
    texlive-fonts-recommended \
    texlive-generic-recommended \
    libxrender1 \    
    && apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN apt-get update && apt-get install -yq --no-install-recommends \
    wget \
    bzip2 \
    ca-certificates \
    sudo \
    locales \
    && apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN echo "en_US.UTF-8 UTF-8" > /etc/locale.gen && \
    locale-gen

# Configure environment
ENV CONDA_DIR /opt/conda
ENV PATH $CONDA_DIR/bin:$PATH
ENV SHELL /bin/bash
ENV LC_ALL en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US.UTF-8

RUN cd /tmp && \
    mkdir -p $CONDA_DIR && \
    wget --quiet https://repo.continuum.io/miniconda/Miniconda3-3.19.0-Linux-x86_64.sh && \
    echo "9ea57c0fdf481acf89d816184f969b04bc44dea27b258c4e86b1e3a25ff26aa0 *Miniconda3-3.19.0-Linux-x86_64.sh" | sha256sum -c - && \
    /bin/bash Miniconda3-3.19.0-Linux-x86_64.sh -f -b -p $CONDA_DIR && \
    rm Miniconda3-3.19.0-Linux-x86_64.sh && \
    $CONDA_DIR/bin/conda install --quiet --yes conda==3.19.1 && \
    $CONDA_DIR/bin/conda config --system --add channels conda-forge && \
    conda install --quiet --yes \
    'ipywidgets=5.1*' \
    'pandas=0.18*' \
    'numexpr=2.5*' \
    'matplotlib=1.5*' \
    'scipy=0.17*' \
    'seaborn=0.7*' \
    'sympy=1.0*' \
    'cython=0.24*' \
    'patsy=0.4*' \
    'cloudpickle=0.1*' \
    'dill=0.2*' \
    'lxml=3.6*' \
    'sqlalchemy=1.0*'\
    'holoviews=1.4.3' \
    'beautifulsoup4=4.4*' \
    'feedparser=5.2*' &&\
    conda install --quiet --yes \
    -c basnijholt 'kwant=1.2.2' &&\
    conda clean -tipsy
