CC=g++

PROJ_ROOT = $(abspath .)
TMP_DIR = $(PROJ_ROOT)/tmp
SRC_DIR = $(PROJ_ROOT)/src
TARGET_DIR = $(PROJ_ROOT)/bin

$(shell if [ ! -e $(TMP_DIR) ];then mkdir -p $(TMP_DIR); fi)
$(shell if [ ! -e $(TARGET_DIR) ];then mkdir -p $(TARGET_DIR); fi)

SRC := $(SRC_DIR)/*.cpp
SRC := $(wildcard ${SRC})
OBJ := $(patsubst ${SRC_DIR}/%.cpp,${TMP_DIR}/%.o,${SRC})

TARGET := ${TARGET_DIR}/main

CFLAGS=-Wall -g

all:$(TARGET)

$(TARGET):$(OBJ)
	$(CC) $^ -o $@

${OBJ}:$(TMP_DIR)/%.o:$(SRC_DIR)/%.cpp
	$(CC) $(CFLAGS) -c $^ -o $@

clean:
	rm $(TMP_DIR)/*.o $(TARGET) -rf

echo:
	@echo PROJ_ROOT: $(PROJ_ROOT)
	@echo TMP_DIR: $(TMP_DIR)
	@echo SRC_DIR: $(SRC_DIR)
	@echo OBJ: $(OBJ)
	@echo SRC: $(SRC)
	@echo TARGET: $(TARGET)
