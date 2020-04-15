FROM 520713654638.dkr.ecr.ap-northeast-1.amazonaws.com/sagemaker-pytorch:1.1.0-cpu-py3

ARG PYTHON_PASS=/usr/bin/python3.6
ENV GIT_SSL_NO_VERIFY=1

# apt install
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
         curl \
         git \
         vim \
         groff-base # awscli

# pip install
COPY requirements.txt /tmp/
RUN $PYTHON_PASS -m pip install --upgrade pip && \
    $PYTHON_PASS -m pip install -r /tmp/requirements.txt

# install gcloud
RUN echo "deb [signed-by=/usr/share/keyrings/cloud.google.gpg] https://packages.cloud.google.com/apt cloud-sdk main" | tee -a /etc/apt/sources.list.d/google-cloud-sdk.list && \
   apt-get install -y apt-transport-https ca-certificates && \
   curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key --keyring /usr/share/keyrings/cloud.google.gpg add - && \
   apt-get update && apt-get install -y google-cloud-sdk

# install docker
RUN curl https://get.docker.com | sh

# make dir
RUN mkdir -p /opt/config \
             /opt/data/raw \
             /opt/data/interim \
             /opt/data/processed \
             /opt/data/external \
             /opt/features \
             /opt/logs \
             /opt/models \
             /opt/notebooks \
             /opt/reports \
             /opt/scripts \
             /opt/utils

# cd
WORKDIR /opt

# expose port TensorBoard
EXPOSE 6006
# expose port TensorBoard
EXPOSE 8888
