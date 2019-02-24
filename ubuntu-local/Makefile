IMAGE := $(notdir $(patsubst %/,%,$(dir $(realpath $(firstword $(MAKEFILE_LIST))))))

run: build
	@docker run -it --rm $(IMAGE)

build:
	@docker build -qt $(IMAGE) . >/dev/null

noisy-rebuild:
	@docker build --no-cache -t $(IMAGE) .

.PHONY: clean
clean:
	@docker rmi $(IMAGE) >/dev/null 2>&1 || true
