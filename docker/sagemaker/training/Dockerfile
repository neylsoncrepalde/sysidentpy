FROM ubuntu:latest
    
# Set a docker label to advertise multi-model support on the container
LABEL com.amazonaws.sagemaker.capabilities.multi-models=false
# Set a docker label to enable container to use SAGEMAKER_BIND_TO_PORT environment variable if present
LABEL com.amazonaws.sagemaker.capabilities.accept-bind-to-port=true

# Install some handful libraries like curl, wget, git, build-essential, zlib
RUN apt-get update && apt-get install -y --no-install-recommends \
        build-essential \
        gcc \
        python3.7 \
        python3-dev \
        python3-pip \
        ca-certificates \
        git \
        curl \
        wget &&\
    rm -rf /var/lib/apt/lists/*

# upgrade pip
RUN pip3 --no-cache-dir install --upgrade pip3

# set some environment variables
ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1 \
    PYTHONIOENCODING=UTF-8 \
    LANG=C.UTF-8 \
    LC_ALL=C.UTF-8

# install sagemaker training and other libraries
RUN pip3 install --no-cache --upgrade \
    boto3 \
    sagemaker \
    sagemaker-training \
    sysidentpy==0.1.8

# Copy the training script to the container
COPY code/train.py opt/ml/code/train.py

# Change the working directory to code folder
WORKDIR /opt/ml/code

# defines train.py as entrypoint
ENV SAGEMAKER_PROGRAM train.py
