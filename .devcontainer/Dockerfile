###################################################
##### SETTING OPERATING SYSTEM #####
###################################################

# This is an official python image.
FROM python:3.11.6-bookworm

# Set the user to root.
USER root

# Prevent interactive popups when initializing debian.
ENV DEBIAN_FRONTEND=noninteractive

# Set up a dir for our stuff
RUN mkdir -p /devcontainer
RUN chmod -R 777 /devcontainer

# Install OS packages
RUN apt-get update && apt-get install -y \
    build-essential \
    curl \
    git \
    cmake \
    wget \
    zsh

###################################################
##### CONFIGURING PYTHON AND INIT SCRIPTS #####
###################################################

# Set up an installation env
COPY ./scripts /devcontainer/init
COPY ./requirements.txt /devcontainer/requirements.txt

# Install python packages
RUN pip install --upgrade pip --disable-pip-version-check
RUN pip install -r /devcontainer/requirements.txt --disable-pip-version-check

# The following will persist shell history between sessions
RUN SNIPPET="export PROMPT_COMMAND='history -a' && export HISTFILE=/commandhistory/.bash_history" \
    && echo "$SNIPPET" >> "/root/.bashrc"

# This works for other shells too, the following works for ZSH.
RUN SNIPPET="export HISTFILE=/commandhistory/.zsh_history; setopt INC_APPEND_HISTORY" \
    && echo "$SNIPPET" >> "/root/.zshrc"