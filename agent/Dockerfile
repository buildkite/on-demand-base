FROM debian:buster-slim

RUN apt-get update && \
    apt-get install -y \
      curl \
      git \
      hub \
      python-pip &&
    rm -rf /var/lib/apt/lists/*

COPY ["ssh", "/root/.ssh"]

RUN pip install awscli~=1.16 --upgrade

RUN cd /tmp && \
    curl --location https://github.com/keithduncan/travis-pipeline/releases/download/v0.5/travis-pipeline_0.5.0_amd64.deb >travis-pipeline_0.5.0_amd64.deb && \
    dpkg -i travis-pipeline_0.5.0_amd64.deb && \
    rm travis-pipeline_0.5.0_amd64.deb
