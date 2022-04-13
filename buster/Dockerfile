FROM debian:buster

RUN apt-get update && apt-get install -y --no-install-recommends \
  python \
  git \
  pkg-config \
  fakeroot \
  rpm \
  sudo \
  apt-transport-https \
  ca-certificates \
  libx11-dev \
  libx11-xcb-dev \
  libxkbfile-dev \
  libsecret-1-dev \
  curl \
  gnupg \
  wget \
  unzip

# Yarn
RUN wget -qO - https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
RUN apt-get update && apt-get install -y yarn
