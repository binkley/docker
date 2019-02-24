FROM ubuntu:devel AS base
RUN { echo y; echo y; } | /usr/local/sbin/unminimize
RUN ["/usr/bin/apt-get", "dist-upgrade"]
RUN ["/usr/bin/apt-get", "install", "--yes", \
    "man-db", "libxss1", "aptitude", "git"]
RUN ["/usr/bin/apt-get", "clean"]

# Leave the apt caches, so that "search" works
# FROM base AS clean
# RUN ["/bin/rm", "-rf", "/var/lib/apt/lists"]

FROM base AS user
COPY bashrc /tmp/bashrc
ARG USER
ENV USER=$USER
RUN useradd -ms /bin/bash $USER
RUN cat /tmp/bashrc >>/home/$USER/.bashrc
RUN rm /tmp/bashrc

FROM user
ARG USER
USER $USER
WORKDIR /home/$USER
CMD ["/bin/bash", "-il"]
