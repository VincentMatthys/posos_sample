NAME = posos-challenge
PWD = $(shell pwd)
UID = $(shell id -u)
GID = $(shell id -g)


.PHONY: test
test:
	UID=$(UID) GID=$(GID) docker-compose build
	UID=$(UID) GID=$(GID) docker-compose up
	UID=$(UID) GID=$(GID) docker-compose down

.PHONY: build_exp
build_exp:
	docker build -f Dockerfile --tag $(NAME)_exp\
			--build-arg uid=$(UID)\
			--build-arg gid=$(GID)\
			.

.PHONY: exp
exp: build_exp clean_exp
	docker run -it --rm\
	        --name=$(NAME)_exp\
	        -v $(PWD):/app\
			-p 8888:8888\
	        $(NAME)_exp:latest\
			"jupyter lab\
				--no-browser\
				--notebook-dir=/app\
				--ip=0.0.0.0\
				--log-level='INFO'"

.PHONY: clean_exp
clean_exp:
	docker rm -f $(NAME)_exp 2> /dev/null || true