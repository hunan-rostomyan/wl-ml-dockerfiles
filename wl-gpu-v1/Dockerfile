from ubuntu:16.04

RUN apt-get update && apt-get install -y --no-install-recommends apt-utils

# Python
RUN apt-get install -y python-pip python3-pip python-dev build-essential
RUN pip install --upgrade pip
RUN apt-get install -y python-virtualenv

# Tensorflow
RUN apt-get install -y libcupti-dev

WORKDIR "/home"

CMD ["/bin/bash"]

