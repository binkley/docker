IMAGE := $(notdir $(patsubst %/,%,$(dir $(realpath $(firstword $(MAKEFILE_LIST))))))

run: build
	@docker run \
	-e TZ=$(shell ./guess-timezone) \
	-it --rm $(IMAGE)

build: Dockerfile bash_aliases bashrc guess-timezone gitconfig
	@docker build \
		--build-arg USER \
		-qt $(IMAGE) . >/dev/null

noisy-rebuild: gitconfig
	@docker build \
		--build-arg USER \
		--no-cache -t $(IMAGE) .

.INTERMEDIATE: gitconfig
gitconfig: pre-gitconfig
	@cp pre-gitconfig $@
	@echo "    name = $(shell git config --global user.name)" >>$@
	@echo "    email = $(shell git config --global user.email)" >>$@

.PHONY: clean
clean:
	@docker rmi $(IMAGE) >/dev/null 2>&1 || true
