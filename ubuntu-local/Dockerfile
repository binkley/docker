FROM ubuntu:disco AS base
RUN { echo y; echo y; } | /usr/local/sbin/unminimize

FROM base AS man-pages
RUN dpkg -l \
    | grep '^ii' \
    | cut -d ' ' -f3 \
    | xargs apt-get install --reinstall --yes
RUN ["/usr/bin/apt-get", "install", "--yes", "man-db"]
RUN ["/bin/rm", "-rf", "/var/lib/apt/lists"]

FROM man-pages
CMD ["/bin/bash", "-il"]
