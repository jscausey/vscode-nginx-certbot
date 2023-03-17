FROM ubuntu:22.04

RUN apt-get update \
    && apt-get install -y --auto-remove \
    curl \
    hugo \
    python3 \
    python3-dev \
    python3-pip \
    unzip \
    wget \
    zip \
    && wget -O- https://aka.ms/install-vscode-server/setup.sh | sh \
    && code-server serve-local --accept-server-license-terms --list-extensions \
    && echo '{"consented":true}' > /root/.vscode-cli/license_consent.json \
    && pip3 install debugpy \
    && code-server serve-local --install-extension ms-python.python

EXPOSE 8000
CMD /usr/local/bin/code-server serve-local --telemetry-level off --host 0.0.0.0 --port 8000 --without-connection-token
