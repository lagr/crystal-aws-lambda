CRYSTAL_BIN ?= $(shell which crystal)
SHARDS_BIN ?= $(shell which shards)

ifeq ($(OS),Windows_NT)
	uname_S := Windows
else
	uname_S := $(shell uname -s)
endif

build:
	[ -d bin ] || mkdir bin
ifeq ($(uname_S), Darwin)
	docker run --rm -it -v $(CURDIR):/app -w /app durosoft/crystal-alpine:0.27.0 /bin/sh -c "crystal build src/bootstrap.cr -o bin/bootstrap --release --static --no-debug ; strip bin/bootstrap"
else
	$(SHARDS_BIN) build --release --static --no-debug $(CRFLAGS)
endif
	zip -j bootstrap.zip bin/bootstrap

dependencies:
	(SHARDS_BIN)

clean:
	rm -fr ./bin bootstrap.zip

test: build
	$(CRYSTAL_BIN) spec
