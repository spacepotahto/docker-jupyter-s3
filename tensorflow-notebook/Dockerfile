FROM jupyter/tensorflow-notebook

# Install boto3
RUN mamba install --quiet --yes \
    'boto3' && \
    mamba clean --all -f -y && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"

# Setup directories
RUN rm -rf "work" && mkdir "models"

# Set given Jupyter password by passing the hash
# of the password to Jupyter
USER root
RUN echo -e '#!/bin/bash \n\n\
HASH_CMD=`cat <<EOF \n\
from jupyter_server.auth import passwd \n\
print(passwd("${JUPYTER_PASSWORD}")) \n\
EOF` \n\
echo $(python -c "$HASH_CMD")' > /usr/local/bin/pw_hash.sh \
&& chmod +x /usr/local/bin/pw_hash.sh
USER ${NB_UID}

CMD start.sh jupyter lab --ServerApp.password=$(pw_hash.sh)