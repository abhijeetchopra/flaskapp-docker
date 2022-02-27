.PHONY: init
init:
		@echo "ERROR: no Makefile target selected"
		@exit 1

.PHONY: list
list:
		@echo "Running containers:"
		@docker ps | grep flask_webapp || true

		@echo "" && echo "Stopped containers:"
		@docker ps -a | grep Exited | grep flask_webapp || true

		@echo "" && echo "Images"
		@docker images | grep flask_webapp || true

.PHONY: build
build:
		@# build container
		VERSION=$$(cat VERSION); docker build -t flask_webapp:$$VERSION .;

.PHONY: start
start:
		@# start container
		VERSION=$$(cat VERSION); docker run -d -p 8000:8000 flask_webapp:$$VERSION;
		@echo "visit http://localhost:8000" && echo ""

.PHONY: stop
stop:
		@# stop container
		VERSION=$$(cat VERSION); docker stop $$(docker container ls | grep flask_webapp | grep $$VERSION | awk '{print $$1}') || true;

.PHONY: remove
remove:
		@# remove container
		VERSION=$$(cat VERSION); docker rm $$(docker container ls --all | grep flask_webapp | grep $$VERSION | awk '{print $$1}') || true;

.PHONY: clean
clean:
		@# stop container
		VERSION=$$(cat VERSION); docker stop $$(docker container ls | grep flask_webapp | grep $$VERSION | awk '{print $$1}') || true;

		@# remove container
		VERSION=$$(cat VERSION); docker rm $$(docker container ls --all | grep flask_webapp | grep $$VERSION | awk '{print $$1}') || true;

		@# remove image
		VERSION=$$(cat VERSION); docker rmi $$(docker image ls | grep flask_webapp | grep $$VERSION | awk '{print $$3}') || true;
