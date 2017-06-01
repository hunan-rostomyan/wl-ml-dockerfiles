from ubuntu:16.04

# Update
RUN apt-get update && apt-get install -y --no-install-recommends apt-utils

# Replace /bin/sh with bash
RUN rm /bin/sh && ln -s /bin/bash /bin/sh

# Utilities
RUN apt-get install -y tree
RUN apt-get install -y vim

# Python
RUN apt-get install -y python-pip python3-pip python-dev build-essential
RUN pip install --upgrade pip
RUN apt-get install -y python-virtualenv

# Tensorflow
RUN apt-get install -y libcupti-dev

WORKDIR /home

# Create a virtual environment
RUN virtualenv --system-site-packages tf

# Activate the venv
RUN source /home/tf/bin/activate

CMD ["/bin/bash"]

