#FROM jupyter/datascience-notebook:95ccda3619d0
FROM jupyter/tensorflow-notebook:42f4c82a07ff

# Remove the manpage blacklist, install man, install docs
#RUN rm /etc/dpkg/dpkg.cfg.d/excludes \
#    && apt-get update \
#    && dpkg -l | grep ^ii | cut -d' ' -f3 | xargs apt-get install -yq --no-install-recommends --reinstall man \
USER root
RUN apt-get update \
    && apt-get install -y \
    git \
    libglib2.0-0 \
    libsm6 \
    libxext6 \
    libxrender1 \
    vim \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Install packages via pip
USER jovyan
COPY --chown=${NB_UID}:${NB_GID} requirements.txt /tmp/
RUN pip install --requirement /tmp/requirements.txt && \
    fix-permissions $CONDA_DIR && \
    fix-permissions /home/$NB_USER
