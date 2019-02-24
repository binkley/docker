IMAGE := $(notdir $(patsubst %/,%,$(dir $(realpath $(firstword $(MAKEFILE_LIST))))))

run: build
	@docker run -it --rm $(IMAGE)

build:
	@docker build -qt $(IMAGE) . >/dev/null
