.PHONY: init

APP_NAME=flask_webapp

init:
		@echo "ERROR: no Makefile target selected"
		@echo ""
		@echo "USAGE: make [list, build, start, stop, remove, clean]"
		@echo ""
		@exit 1

.PHONY: list
list:
		@echo "Running containers:"
		@docker ps | grep $(APP_NAME) || true

		@echo "" && echo "Stopped containers:"
		@docker ps -a | grep Exited | grep $(APP_NAME) || true

		@echo "" && echo "Images:"
		@docker images | grep $(APP_NAME) || true

.PHONY: build
build:
		@# build container
		@FILE_VERSION=$$(cat VERSION); \
		echo "Enter version to build...(leave blank to read from VERSION file which currently is: $$FILE_VERSION)"; \
		read READ_VERSION; \
		echo $$READ_VERSION; \
		echo $$FILE_VERSION; \
		VERSION=$${READ_VERSION:-$$FILE_VERSION}; \
		docker build -t $(APP_NAME):$$VERSION .;

.PHONY: start
start:
		@# start container
		@FILE_VERSION=$$(cat VERSION); \
		echo "Enter version to start...(leave blank to read from VERSION file which currently is: $$FILE_VERSION)"; \
		read READ_VERSION; \
		echo $$READ_VERSION; \
		echo $$FILE_VERSION; \
		VERSION=$${READ_VERSION:-$$FILE_VERSION}; \
		docker run -d -p 8000:8000 $(APP_NAME):$$VERSION;
		@echo "visit http://localhost:8000" && echo ""

.PHONY: stop
stop:
		@# stop container
		@VERSION=$$(cat VERSION); docker stop $$(docker container ls | grep $(APP_NAME) | grep $$VERSION | awk '{print $$1}') || true;

.PHONY: remove
remove:
		@# remove container
		@VERSION=$$(cat VERSION); docker rm $$(docker container ls --all | grep $(APP_NAME) | grep $$VERSION | awk '{print $$1}') || true;

.PHONY: clean
clean:
		@# stop container
		@VERSION=$$(cat VERSION); docker stop $$(docker container ls | grep $(APP_NAME) | grep $$VERSION | awk '{print $$1}') || true;

		@# remove container
		@VERSION=$$(cat VERSION); docker rm $$(docker container ls --all | grep $(APP_NAME) | grep $$VERSION | awk '{print $$1}') || true;

		@# remove image
		@VERSION=$$(cat VERSION); docker rmi $$(docker image ls | grep $(APP_NAME) | grep $$VERSION | awk '{print $$3}') || true;
