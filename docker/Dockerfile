# Start with BioSim base image.
ARG BASE_IMAGE=latest
FROM ghcr.io/ccpbiosim/jupyterhub-base:$BASE_IMAGE

LABEL maintainer="James Gebbie-Rayet <james.gebbie@stfc.ac.uk>"
LABEL org.opencontainers.image.source=https://github.com/ccpbiosim/clustering-workshop
LABEL org.opencontainers.image.description="A container environment for the ccpbiosim workshop on Clustering."
LABEL org.opencontainers.image.licenses=MIT

# Switch to jovyan user.
USER $NB_USER
WORKDIR $HOME

# Install workshop deps
RUN conda install matplotlib numpy scipy ipywidgets -y
RUN pip install mdplus mdtraj rlcluster

# Get workshop files and move them to jovyan directory.
COPY --chown=1000:100 . .
RUN rm -rf requirements.txt AUTHORS LICENSE README.md docker .git .github

# Copy updated lab workspace
COPY --chown=1000:100 docker/default-37a8.jupyterlab-workspace /home/jovyan/.jupyter/lab/workspaces/default-37a8.jupyterlab-workspace

# UNCOMMENT THIS LINE FOR REMOTE DEPLOYMENT
COPY docker/jupyter_notebook_config.py /etc/jupyter/

# Always finish with non-root user as a precaution.
USER $NB_USER
