FROM ubuntu:devel AS base
RUN { echo y; echo y; } | /usr/local/sbin/unminimize

FROM base AS man-pages
RUN dpkg -l \
    | grep '^ii' \
    | cut -d ' ' -f3 \
    | xargs apt-get install --reinstall --yes
RUN ["/usr/bin/apt-get", "install", "--yes", "man-db"]

FROM man-pages AS aptitude
RUN ["/usr/bin/apt-get", "install", "--yes", "libxss1"]
RUN ["/usr/bin/apt-get", "install", "--yes", "aptitude"]

FROM aptitude AS clean
RUN ["/bin/rm", "-rf", "/var/lib/apt/lists"]

FROM clean
CMD ["/bin/bash", "-il"]
