FROM debian

# Common Development Tools
RUN apt-get update && \
    apt-get -y install \
    build-essential gdb curl wget git sudo gpg tzdata xz-utils \
    python3 python3-pip python3-venv python3-dev

# Python Setup
RUN python3 -m pip install --upgrade pip &&\
    python3 -m pip install python-language-server[all]

# Install code-server
RUN curl -fsSL https://code-server.dev/install.sh | sh

# User Account
RUN adduser --disabled-password --gecos '' coder && \
    adduser coder sudo && \
    echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

USER coder

# Environment
ENV SHELL=/bin/bash \
    LC_ALL=C.UTF-8 \
    LANG=C.UTF-8 \
    TZ=US/Eastern

# Entry Point
EXPOSE 3000
WORKDIR /home/coder
ENTRYPOINT ["code-server"]
CMD []
