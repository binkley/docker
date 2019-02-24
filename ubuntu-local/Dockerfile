FROM ubuntu:disco AS base
RUN ["/usr/bin/apt-get", "update"]
RUN ["/usr/bin/apt-get", "--yes", "upgrade"]
RUN ["/bin/rm", "/etc/dpkg/dpkg.cfg.d/excludes"]
RUN dpkg -l \
    | grep '^ii' \
    | cut -d ' ' -f3 \
    | xargs apt-get install --reinstall --yes
RUN ["/usr/bin/apt-get", "install", "--yes", "man-db"]
RUN echo y | unminimize >/dev/null
RUN ["/bin/rm", "-rf", "/var/lib/apt/lists"]

CMD ["/bin/bash", "-il"]
