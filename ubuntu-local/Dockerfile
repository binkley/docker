FROM ubuntu:devel AS base
RUN { echo y; echo y; } | /usr/local/sbin/unminimize
RUN ["/usr/bin/apt-get", "dist-upgrade"]
RUN ["/usr/bin/apt-get", "install", "--yes", \
    "man-db", "libxss1", "aptitude", "git"]
RUN ["/usr/bin/apt-get", "clean"]

# Leave the apt caches, so that "search" works
# FROM base AS clean
# RUN ["/bin/rm", "-rf", "/var/lib/apt/lists"]

ARG USER
FROM base AS user
ARG USER
ENV USER=$USER
RUN useradd -ms /bin/bash $USER
# COPY --chown=$USER:$USER bashrc /tmp/ - TODO: https://github.com/moby/moby/issues/35018
COPY bashrc /tmp/
COPY inputrc /tmp/
RUN cat /tmp/bashrc >>/home/$USER/.bashrc
RUN cat /tmp/inputrc >>/home/$USER/.inputrc
RUN rm /tmp/bashrc
RUN rm /tmp/inputrc

FROM user
ARG USER
USER $USER
WORKDIR /home/$USER
CMD ["/bin/bash", "-il"]
