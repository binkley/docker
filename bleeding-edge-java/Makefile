IMAGE := $(notdir $(patsubst %/,%,$(dir $(realpath $(firstword $(MAKEFILE_LIST))))))

run: build
	@docker run \
	-e LANG \
	-e TZ=$(shell ./guess-timezone) \
	-it --rm $(IMAGE)

build: pull Dockerfile bash_aliases bashrc guess-timezone gitconfig
	@docker build \
		--build-arg LANG \
		--build-arg USER \
		-qt $(IMAGE) . >/dev/null

noisy-rebuild: pull gitconfig
	@docker build \
		--build-arg LANG \
		--build-arg USER \
		--no-cache -t $(IMAGE) .

pull:
	@docker pull adoptopenjdk/openjdk11-openj9:latest

.INTERMEDIATE: gitconfig
gitconfig: pre-gitconfig
	@cp pre-gitconfig $@
	@echo "    name = $(shell git config --global user.name)" >>$@
	@echo "    email = $(shell git config --global user.email)" >>$@

.PHONY: clean
clean:
	@docker rmi $(IMAGE) >/dev/null 2>&1 || true
