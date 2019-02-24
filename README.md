<img src="https://i2.wp.com/blog.docker.com/wp-content/uploads/2013/06/Docker-logo-011.png"
alt="Docker" align="right" height="20%" width="20%"/>
<img src="https://random-octodex.herokuapp.com/random" alt="Octodex"
align="right" height="20%" width="20%"/>

# Docker

Custom docker images

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

## Images

* [ubuntu-local](ubuntu-local/)
