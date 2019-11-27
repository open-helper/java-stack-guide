# ####################################
# log4j/pjg AREA
# ####################################

SRC_PROJ_HOME	:= ..


# ####################################
# Dashboard AREA
# ####################################
build:
	cd $(SRC_PROJ_HOME) && mvn clean package -Dmaven.test.skip=true

install:
	cd $(SRC_PROJ_HOME) && mvn clean install -Dmaven.test.skip=true

dispatch:
	cd $(SRC_PROJ_HOME) && find . -name "Dockerfile" -o -name "*.sql" | xargs -t tar -cf- | tar -xvf- -C ../../../apps/docker-compose/log4j-pig/stub


# ####################################
# Utils AREA
# ####################################
clean:
	cd $(SRC_PROJ_HOME) && mvn clean
	rm -rvf $(SRC_PROJ_HOME)/*.bak $(SRC_PROJ_HOME)/*.log
