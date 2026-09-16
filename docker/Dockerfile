# Start with BioSim base image.
ARG BASE_IMAGE=latest@sha256:5eb67b09e3fdf64b3128bd9501e08a0cbb007804b678f2096728d8c1260e6217
FROM ghcr.io/ccpbiosim/jupyterhub-base:$BASE_IMAGE

LABEL maintainer="James Gebbie-Rayet <james.gebbie@stfc.ac.uk>"

# Switch to jovyan user.
USER $NB_USER
WORKDIR $HOME

# Install workshop deps
RUN conda install -y -c conda-forge \
    conda-forge::matplotlib=3.11.1 \
    conda-forge::numpy=2.5.3 \
    conda-forge::scipy=1.18.1 \
    conda-forge::ipywidgets=8.1.9
RUN pip install --no-cache-dir \
    mdtraj==1.11.1.post2 \
    mdplus==0.1.2 \
    rlcluster==0.0.5

# Get workshop files and move them to jovyan directory.
COPY --chown=1000:100 . .
RUN rm -rf requirements.txt AUTHORS LICENSE README.md docker .git .github

# Copy updated lab workspace
COPY --chown=1000:100 docker/default-37a8.jupyterlab-workspace /home/jovyan/.jupyter/lab/workspaces/default-37a8.jupyterlab-workspace

# Always finish with non-root user as a precaution.
USER $NB_USER
