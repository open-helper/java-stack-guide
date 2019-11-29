# ####################################
# @file: Makefile
# @name: log4j-pig-ui
# @date: 2019-11-29 22:36:02
# @tver: 20191129
# ####################################


DK      := docker
DC      := docker-compose
DK_EXEC := docker exec -it

DATA_SUF       := $(shell date +"%Y.%m.%d.%H.%M.%S")
DK_FILE        := ./Dockerfile
DK_IMG_PREFIX  := open-helper


# ####################################
# Dashboard AREA
# ####################################
build:
	$(call genNodeDockerfile,$(DK_FILE))
	docker build -t $(DK_IMG_PREFIX)/log4j-pig/pig-ui -f $(DK_FILE) ..

status:
	docker images | grep $(DK_IMG_PREFIX)


# ####################################
# Utils AREA
# ####################################
clean:
	rm -rvf *.bak *.log
	-$(DK) ps -a | grep Exited | awk '{print $$1}' | xargs $(DK) rm
	-$(DK) images | grep "^<none>" | awk '{print $$3}' | xargs $(DK) rmi

# 基于onbuild生成Node专用的Dockerfile
define genNodeDockerfile
	echo "FROM open-helper/1st/node-onbuild" > $(1)
endef
