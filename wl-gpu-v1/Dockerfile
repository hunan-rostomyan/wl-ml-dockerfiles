from ubuntu:16.04

# Update
RUN apt-get update && apt-get install -y --no-install-recommends apt-utils

# Replace /bin/sh with bash
RUN rm /bin/sh && ln -s /bin/bash /bin/sh

# Utilities
RUN apt-get install -y wget
RUN apt-get install -y tree
RUN apt-get install -y vim

# Python
RUN apt-get install -y python-pip python3-pip python-dev build-essential
RUN apt-get install -y python3-tk
RUN pip install --upgrade pip
RUN pip3 install --upgrade pip
RUN apt-get install -y python-virtualenv

# Tensorflow prep
RUN apt-get install -y libcupti-dev

WORKDIR /home

# Create a virtual environment
RUN virtualenv --system-site-packages tf

# Activate the venv
RUN source /home/tf/bin/activate

# Install Tensorflow
RUN pip3 install --upgrade tensorflow-gpu

# Install CUDA toolkit
RUN mkdir /tmp/cuda_install
WORKDIR /tmp/cuda_install
RUN wget http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/cuda-repo-ubuntu1604_8.0.61-1_amd64.deb
RUN dpkg -i cuda-repo-ubuntu1604_8.0.61-1_amd64.deb
RUN apt-get update

# workaround: take care of packages with interactive parts
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y tzdata
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y keyboard-configuration
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y cuda

# install CUDA neural networks library
COPY cudnn-8.0-linux-x64-v6.0.tgz /tmp/cuda_install
RUN tar -xzvf cudnn-8.0-linux-x64-v6.0.tgz
RUN cp cuda/lib64/libcudnn* /usr/local/cuda-8.0/lib64/
RUN cp cuda/include/cudnn.h /usr/local/cuda-8.0/include

# fix the dynamic library issue
RUN ln -s /usr/local/cuda-8.0/lib64/libcudnn.so /usr/local/cuda-8.0/lib64/libcudnn.so.5

# clean up
RUN rm -rf /tmp/cuda_install

WORKDIR /home

CMD ["/bin/bash"]

