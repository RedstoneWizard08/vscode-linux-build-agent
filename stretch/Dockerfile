FROM debian:stretch

RUN apt-get update && apt-get install -y --no-install-recommends \
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
  unzip \
  # Dependencies for building python from source
  build-essential \
  libreadline-gplv2-dev \
  libncursesw5-dev \
  libssl-dev \
  libsqlite3-dev \
  tk-dev \
  libgbm-dev \
  libc6-dev \
  libbz2-dev \
  libffi-dev \
  zlib1g-dev

# Compile python3.9 from source
RUN curl -O https://www.python.org/ftp/python/3.9.4/Python-3.9.4.tar.xz
RUN tar -xf Python-3.9.4.tar.xz
RUN cd Python-3.9.4 && ./configure --enable-optimizations && make altinstall
RUN update-alternatives --install /usr/bin/python python /usr/local/bin/python3.9 1
RUN python --version

# Remove expired CA cert for openSSL 1.0.2
# https://www.openssl.org/blog/blog/2021/09/13/LetsEncryptRootCertExpire/
RUN rm -f /usr/share/ca-certificates/mozilla/DST_Root_CA_X3.crt
RUN update-ca-certificates --fresh

# Yarn
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
RUN apt-get update && apt-get install -y yarn

# Add backports
# Required for github action https://github.com/actions/checkout/issues/126#issuecomment-570288731
RUN echo "deb http://deb.debian.org/debian stretch-backports main" | sudo tee -a /etc/apt/sources.list.d/backports.list
RUN apt-get update && apt-get install -y -t stretch-backports git git-man
