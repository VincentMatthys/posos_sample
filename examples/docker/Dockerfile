# Use the official docker image for python3.7
FROM python:3.7

# Define uid and gid arguments (passed during docker build command)
ARG user=appuser
ARG group=appuser
ARG uid
ARG gid

# Add in the container the group and the user you filled in
# https://docs.docker.com/develop/develop-images/dockerfile_best-practices/
RUN groupadd -g ${gid} ${group}
RUN useradd -u ${uid} -g ${group} ${user} -m

# Give the created home the proper rights
RUN chown -R ${user}:${group} /home/${user}

# Add the user bin path in global PATH
ENV PATH="/home/${user}/.local/bin/:${PATH}"

# Change user
USER appuser

# Install jupyterlab in container
RUN pip3 install --user jupyterlab
# Install python packages
RUN pip3 install --user sklearn
RUN pip3 install --user "dask[complete]"
RUN pip3 install --user annoy

# When the container launches, launches a jupyterlab instance
CMD ["jupyter", "lab", "--no-browser", "--notebook-dir='/home/appuser'", "--ip=0.0.0.0", "--log-level='INFO'"]