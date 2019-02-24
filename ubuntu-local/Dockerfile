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
ARG USER
RUN useradd -ms /bin/bash $USER

FROM user
ENV USER=$USER
RUN echo $USER
RUN id
USER $USER
RUN id
WORKDIR /home/$USER
CMD ["/bin/bash", "-il"]
