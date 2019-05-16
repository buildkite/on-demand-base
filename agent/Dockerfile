FROM ubuntu:18.04

RUN apt-get update && \
    apt-get install -y \
      apt-transport-https \
      curl \
      git \
      python-pip

COPY ["buildkite-agent.list", "/etc/apt/sources.list.d/"]
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 32A37959C2FA5C3C99EFBC32A79206696452D198 && \
    apt-get update -o Dir::Etc::sourcelist="sources.list.d/buildkite-agent.list" -o Dir::Etc::sourceparts="-" -o APT::Get::List-Cleanup="0" && \
	  apt-get install -y buildkite-agent
ENV BUILDKITE_BUILD_PATH=/var/lib/buildkite-agent/builds

COPY ["ssh", "/root/.ssh"]

RUN pip install awscli~=1.16 --upgrade

RUN cd /tmp && \
    curl --location https://github.com/keithduncan/travis-pipeline/releases/download/v0.4/travis-pipeline_0.4.0_amd64.deb >travis-pipeline_0.4.0_amd64.deb && \
    dpkg -i travis-pipeline_0.4.0_amd64.deb && \
    rm travis-pipeline_0.4.0_amd64.deb

LABEL buildkite.metadata=awscli,awscli:version=1.16,travis-pipeline,travis-pipeline:version=0.4

ENTRYPOINT ["/usr/bin/buildkite-agent"]
CMD ["start"]
