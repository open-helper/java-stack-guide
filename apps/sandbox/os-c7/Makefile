# ####################################
# Name: log4j-pig
# FileVersion: 20191127
# ####################################


DK	:= docker
DC	:= docker-compose
DK_EXEC := docker exec -it -u foobar

DATA_SUF = $(shell date +"%Y.%m.%d.%H.%M.%S")

include ./.env


# ####################################
# Dashboard AREA
# ####################################
start: init-dir
	$(DC) up -d
stop:
	$(DC) down
config:
	$(DC) config

sh:
	$(DK_EXEC) c7-s1 bash
bash: sh

rebuild-then-start: stop init-dir
	$(DK) images | grep -q $(OS_IMG_TAG) && $(DK) rmi $(OS_IMG_TAG) || true
	$(DC) up --build -d


# ####################################
# Init AREA
# 	init-dir: 
# ####################################
init-dir:
	# 创建数据目录
	for x in $(shell sed -n "/# DATA-DIR-BEGIN/,/# DATA-DIR-END/p" .gitignore | grep -v "#"); do \
		echo "verify dir $$x"; \
		[ -d "$$x" ] || mkdir -p "$$x"; \
	done;
	# 给集群配置文件加上读权限，否则会因用户id不同，导致配置读取不生效
	find conf -name "*.cnf" -exec chmod +r {} \;
	# log目录可写
	chmod o+w ../../../log/os-c7


# ####################################
# Utils AREA
# ####################################
clean:
	rm -rvf log/* *.bak
