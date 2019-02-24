<a href="https://www.docker.com/" title="Docker"><img
src="https://www.docker.com/sites/default/files/social/docker_facebook_share.png"
alt="Docker" align="right" height="20%" width="20%"/></a>
<a href="https://github.com/" title="GitHub"><img
src="https://random-octodex.herokuapp.com/random" alt="Octodex" align="right"
height="20%" width="20%"/></a>

# Docker

Custom docker images

## Images

* [ubuntu-local](ubuntu-local/)

## Using

Each image's `Makefile` provides a **run** target, the default, which
[_builds_](#building), and then opens a shell in that image:

```sh
cd _image name_
make
```

## Building

Each image's `Makefile` provides a **build** target:

```sh
cd _image name_
make build
```

To see what really happens, even on previously built images, consider the
**noisy-rebuild** target, which is slow and noisy.

## Undoing

Each image's `Makefile` provides a **clean** target, to remove the installed
image:

```sh
cd _image name_
make clean
```
