###############
## VARIABLES ##
###############
# Note: Variables can only be strings
# Note: Single or double quotes for variable names or values have no meaning to Make

# CC: Program for compiling C programs; default cc
# CXX: Program for compiling C++ programs; default g++
# CFLAGS: Extra flags to give to the C compiler
# CXXFLAGS: Extra flags to give to the C++ compiler
# CPPFLAGS: Extra flags to give to the C preprocessor
# LDFLAGS: Extra flags to give to the linker

# make build DEBUG=1 to enable GDB
DEBUG ?= 1

# warning options
ENABLE_WARNINGS ?= 1
WARNING_AS_ERRORS ?= 1

# directories
INCLUDE_DIR = include
SOURCE_DIR = src
BUILD_DIR = build

ifeq ($(ENABLE_WARNINGS), 1)
CXX_WARNINGS = -Wall -Wextra
else
CXX_WARNINGS = 
endif

ifeq ($(WARNING_AS_ERRORS), 1)
CXX_WARNINGS += -Werror
endif

CXX_STANDARD ?= c++20 # make build CXX_STANDARD=c++(version)
CXX = g++
CC = gcc
CXXFLAGS = $(CXX_WARNINGS) -std=$(CXX_STANDARD)
CPPFLAGS = -I $(INCLUDE_DIR)
LDFLAGS = -lm

# if-else condition
ifeq ($(DEBUG), 1)
CXXFLAGS += -g -O0
TARGET = debug_code
else
CXXFLAGS += -O3 
TARGET = release_code
endif

COMPILER_CALL = $(CXX) $(CXXFLAGS) $(CPPFLAGS)

SOURCES = $(wildcard $(SOURCE_DIR)/*.cc)
OBJS = $(patsubst $(SOURCE_DIR)/%.cc, $(BUILD_DIR)/%.o, $(SOURCES)) # use patsubst becasue .o files aren't generated yet

##############
##  TARGET 	##
##############
all: create build

build: $(OBJS)
	$(COMPILER_CALL) $(OBJS) $(LDFLAGS) -o $(BUILD_DIR)/$(TARGET)

create:
	@mkdir -p $(BUILD_DIR)

execute:
	./$(BUILD_DIR)/$(TARGET)

clean:
	rm -f $(BUILD_DIR)/*~ 
	rm -f $(BUILD_DIR)/*.o 
	rm -f $(BUILD_DIR)/$(TARGET)
	rm -r $(BUILD_DIR)

##############
## PATTERNS ##
##############
# $@: the file name of the target
# $<: the name of the first dependency
# $^: the names of all prerequisites
$(BUILD_DIR)/%.o: $(SOURCE_DIR)/%.cc
	$(COMPILER_CALL) -c $< -o $@

##############
##  PHONY   ##
##############
.PHONY: build all create execute clean