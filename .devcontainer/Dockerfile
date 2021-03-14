FROM ubuntu:bionic

# Use bash not sh
RUN rm /bin/sh && ln -s /bin/bash /bin/sh

# Install required dev packages, plus curl/certs/zip for sdkman
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends git curl ca-certificates unzip zip

# Install SDKMan
RUN curl -s "https://get.sdkman.io" | bash

# Source SDKMan so we can run `sdk`, then use this to install java 8 and sbt. Note this needs to be in the same RUN command to retain the environment.
RUN source "$HOME/.sdkman/bin/sdkman-init.sh"; sdk install java $(sdk list java | grep -o "8\.[0-9]*\.[0-9]*\.hs-adpt" | head -1); sdk install sbt

# Install node and npm
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends gnupg
RUN curl -sL https://deb.nodesource.com/setup_14.x  | bash -
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install nodejs

# Install yarn and expo-cli using npm
RUN npm install --global yarn expo-cli