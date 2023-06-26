FROM gcr.io/envoy-ci/envoy-build:142e6d5662b98277a84c327da26ed266ab0e3191

ARG USERNAME=vscode
ARG USER_UID=501
ARG USER_GID=$USER_UID

ENV BUILD_DIR=/build
ENV ENVOY_STDLIB=libstdc++

ENV DEBIAN_FRONTEND=noninteractive
RUN echo "deb https://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse" >/etc/apt/sources.list
RUN echo "deb https://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse" >>/etc/apt/sources.list
RUN echo "deb https://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse" >>/etc/apt/sources.list
RUN echo "deb https://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse" >>/etc/apt/sources.list
RUN echo "deb https://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse" >>/etc/apt/sources.list
RUN curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key --keyring /usr/share/keyrings/cloud.google.gpg add -
RUN sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys B53DC80D13EDEF05 \
  && apt-get -y update \
  && apt-get -y install --no-install-recommends libpython2.7 net-tools psmisc vim 2>&1 \
  # Create a non-root user to use if preferred - see https://aka.ms/vscode-remote/containers/non-root-user.
  && groupadd --gid $USER_GID $USERNAME \
  && useradd -s /bin/bash --uid $USER_UID --gid $USER_GID -m $USERNAME -G pcap -d /build \
  # [Optional] Add sudo support for non-root user
  && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
  && chmod 0440 /etc/sudoers.d/$USERNAME

ENV DEBIAN_FRONTEND=
ENV PATH=/opt/llvm/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

ENV CLANG_FORMAT=/opt/llvm/bin/clang-format
