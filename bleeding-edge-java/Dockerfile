FROM adoptopenjdk/openjdk11-openj9:latest AS base
# The DEBIAN_FRONTEND env var setting keeps tzdata from prompting on install
ENV DEBIAN_FRONTEND=noninteractive
RUN yes | /usr/local/sbin/unminimize \
    && /usr/bin/apt-get dist-upgrade \
    && /usr/bin/apt-get install --yes \
    man-db libxss1 aptitude sudo locales tzdata \
    git less vim \
    && /usr/bin/apt-get clean

# Leave the apt caches, so that "search" works
# FROM base AS clean
# RUN ["/bin/rm", "-rf", "/var/lib/apt/lists"]

FROM base AS user
ARG LANG
ENV LANG=$LANG
ARG USER
ENV USER=$USER
# TODO: How to do this dynamically, at run, not build
RUN locale-gen $LANG
RUN useradd -G sudo -ms /bin/bash $USER \
    && echo "$USER ALL=(ALL) NOPASSWD: ALL" >/etc/sudoers.d/$USER \
    && chmod ug=r,o= /etc/sudoers.d/$USER
USER $USER:$USER
COPY bash_aliases /home/$USER/bash_aliases
RUN cat /home/$USER/bash_aliases >>/home/$USER/.bash_aliases \
    && rm /home/$USER/bash_aliases
COPY bashrc /home/$USER/bashrc
RUN cat /home/$USER/bashrc >>/home/$USER/.bashrc \
    && rm /home/$USER/bashrc
COPY gitconfig /home/$USER/gitconfig
RUN cat /home/$USER/gitconfig >>/home/$USER/.gitconfig \
    && rm /home/$USER/gitconfig
COPY inputrc /home/$USER/inputrc
RUN cat /home/$USER/inputrc >>/home/$USER/.inputrc \
    && rm /home/$USER/inputrc

FROM user
ARG USER
USER $USER:$USER
WORKDIR /home/$USER
CMD ["/bin/bash", "-il"]
