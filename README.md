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

## Images

* [ubuntu-local](ubuntu-local/)
