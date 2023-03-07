FROM nvcr.io/nvidia/pytorch:23.02-py3 as base
LABEL maintainer="espen@fastmail.com"
LABEL version="0.1"

ENV CONTAINER_USER=espen \
    CONTAINER_GROUP=espen

ENV PYTHONFAULTHANDLER=1 \
    PYTHONHASHSEED=random \
    PYTHONUNBUFFERED=1

WORKDIR /workspace

ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get update
#RUN apt-get --yes upgrade
RUN apt-get --yes install sudo python3.8-venv gcc dcm2niix

RUN useradd --home /workspace --uid 1000 -U $CONTAINER_USER
RUN mkdir -p /workspace/.local/bin
RUN mkdir /workspace/code
RUN mkdir /workspace/.cache
RUN chown -R $CONTAINER_USER:$CONTAINER_GROUP /workspace
VOLUME /workspace/code
VOLUME /workspace/.cache

USER $CONTAINER_USER:$CONTAINER_GROUP
ENV POETRY_VERSION="1.4.0" \
    PATH=/workspace/.local/bin:$PATH
RUN pip install pipx
RUN pipx install poetry=="$POETRY_VERSION"
