VERSION=v0.1.0
SERVICE_NAME=boilerplate
DOCKER_TAG:=$(SERVICE_NAME):latest
.PHONY: all build docker test run run-docker lint yamllint clean

# Need this because OS-X sed sucks, it doesn't have in-place
SEDCMD := sed
UNAME_S := $(shell uname -s)
ifeq ($(UNAME_S),Darwin)
	SEDCMD := gsed
endif


all: build docker run-docker

build:
	npm run build

docker:
	docker build --tag "$(DOCKER_TAG)" .

test:
	echo "Please write tests here"
	ls -la boilerplate #This will fail if the file doesn't exist

run:
	./boilerplate

run-docker:
	docker stop $(SERVICE_NAME) 2>/dev/null | true
	docker rm $(SERVICE_NAME) 2>/dev/null | true
	docker run -d -p 8080:8080 --name $(SERVICE_NAME) $(DOCKER_TAG)

# Run any lints
lint: yamllint

yamllint:
	# This runs yamllint against everything yaml in this repo, it will exitcode !0 if it fails
	yamllint -c .yamllint.yaml ./

clean:
	# This strips trailing spaces
	find  ./ \( -iname "*.yaml" -o -iname "*.yml" \) -exec ${SEDCMD} -i 's/[[:space:]]*$$//' {} \;
	# Todo add others?