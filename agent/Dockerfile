FROM debian:buster-slim

RUN apt-get update && \
    apt-get install -y \
      curl \
      git \
      hub \
      python-pip \
      socat && \
    rm -rf /var/lib/apt/lists/*

COPY ["ssh", "/root/.ssh"]

ARG AWS_CLI=1.16
RUN pip install awscli~="$AWS_CLI" --upgrade

ARG TRAVIS_PIPELINE=0.5.0
RUN mkdir -p /tmp/travis && \
    cd /tmp/travis && \
    curl --location "https://github.com/keithduncan/travis-pipeline/releases/download/v${TRAVIS_PIPELINE}/travis-pipeline_${TRAVIS_PIPELINE}_amd64.deb" >travis.deb && \
    dpkg -i travis.deb && \
    rm travis.deb

RUN curl --location "https://github.com/buildkite/github-release/releases/download/v1.0/github-release-linux-amd64" >/usr/bin/github-release

ARG COMMIT
ENV BUILDKITE_ABOUT_IMAGE "keithduncan/buildkite-agent\ncommit: $COMMIT\n\naws-cli: $AWS_CLI\ntravis-pipeline: $TRAVIS_PIPELINE\nhub\nsocat"