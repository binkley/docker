FROM ubuntu:devel AS base
RUN yes | /usr/local/sbin/unminimize \
    && /usr/bin/apt-get dist-upgrade \
    && /usr/bin/apt-get install --yes man-db libxss1 aptitude git sudo \
    && /usr/bin/apt-get clean

# Leave the apt caches, so that "search" works
# FROM base AS clean
# RUN ["/bin/rm", "-rf", "/var/lib/apt/lists"]

FROM base AS user
ARG USER
ENV USER=$USER
RUN useradd -ms /bin/bash $USER
COPY bashrc /home/$USER/.bashrc
COPY inputrc /home/$USER/.inputrc
RUN chown $USER:$USER /home/$USER/.bashrc /home/$USER/.inputrc

FROM user
ARG USER
USER $USER
WORKDIR /home/$USER
CMD ["/bin/bash", "-il"]
