FROM ubuntu:18.10 AS base
RUN ["/usr/bin/apt-get", "update"]
RUN ["/bin/rm", "/etc/dpkg/dpkg.cfg.d/excludes"]
RUN dpkg -l \
    | grep '^ii' \
    | cut -d ' ' -f3 \
    | xargs apt-get install --reinstall --yes
RUN ["/usr/bin/apt-get", "install", "--yes", "man-db"]
RUN echo y | unminimize
RUN rm -r /var/lib/apt/lists/*

CMD ["/bin/bash", "-il"]
