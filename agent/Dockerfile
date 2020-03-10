FROM debian:buster-slim

RUN apt-get update && \
    apt-get install -y \
      curl \
      git \
      hub \
      python-pip && \
    rm -rf /var/lib/apt/lists/*

COPY ["ssh", "/root/.ssh"]

ARG AWS_CLI=1.16
RUN pip install awscli~="$AWS_CLI" --upgrade

ARG TRAVIS_PIPELINE=v0.5.0
RUN mkdir -p /tmp/travis-pipeline && \
	cd /tmp/travis-pipeline && \
    curl --location "https://github.com/keithduncan/travis-pipeline/releases/download/${TRAVIS_PIPELINE}/travis-pipeline_${TRAVIS_PIPELINE}_amd64.deb" >travis-pipeline.deb && \
    dpkg -i travis-pipeline.deb && \
    rm travis-pipeline.deb

ENV BUILDKITE_ABOUT_IMAGE "buildkite-agent\naws-cli: $AWS_CLI\ntravis-pipeline: $TRAVIS_PIPELINE\nhub"