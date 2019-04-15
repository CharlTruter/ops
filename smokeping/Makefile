#!/bin/bash

# So we can use the source command
SHELL := /bin/bash

master-build: master-image-build master-image-push
slave-build: slave-image-build slave-image-push
master-image-build:
	source ./env.sh && docker build --build-arg smokeping_slave_name=$$SMOKEPING_NODE --build-arg smokeping_slave_secret=$$SMOKEPING_SECRET -f Dockerfile.master -t $$DOCKER_USER/$$DOCKER_MASTER_REPOSITORY .
master-image-push:
	source ./env.sh && docker push $$DOCKER_USER/$$DOCKER_MASTER_REPOSITORY
master:
	source ./env.sh && docker-compose up -d master
slave-image-build:
	source ./env.sh && docker build --build-arg smokeping_url=$$SMOKEPING_URL --build-arg smokeping_slave_secret=$$SMOKEPING_SECRET --build-arg smokeping_slave_name=$$SMOKEPING_NODE  -f Dockerfile.slave -t $$DOCKER_USER/$$DOCKER_SLAVE_REPOSITORY .
slave-image-push:
	source ./env.sh && docker push $$DOCKER_USER/$$DOCKER_SLAVE_REPOSITORY
slave:
	source ./env.sh && docker-compose up -d slave