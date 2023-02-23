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
DEBUG ?= 0

# warning options
ENABLE_WARNINGS ?= 1
WARNING_AS_ERRORS ?= 1

# header files directories
DRIVER1_INCLUDE = Driver1/include
DRIVER2_INCLUDE = Driver2/include

# source files directories
SOURCE_DIR1 = Driver1/src
SOURCE_DIR2 = Driver2/src

# build directories
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
CPPFLAGS = -I $(DRIVER1_INCLUDE) -I $(DRIVER2_INCLUDE) # include extra header files
LDFLAGS = -lm

ifeq ($(DEBUG), 1)
CXXFLAGS += -g -O0
TARGET = debug_code
else
CXXFLAGS += -O3 
TARGET = release_code
endif

COMPILER_CALL = $(CXX) $(CXXFLAGS) $(CPPFLAGS)

# source file targets from each folder
DRIVER1_SOURCES = $(wildcard $(SOURCE_DIR1)/*.cc)
DRIVER2_SOURCES = $(wildcard $(SOURCE_DIR2)/*.cc)
PROJECT = $(wildcard *.cc)

# replace .cc files with .o files
OBJS1 = $(patsubst $(SOURCE_DIR1)/%.cc, $(BUILD_DIR)/%.o, $(DRIVER1_SOURCES))
OBJS2 = $(patsubst $(SOURCE_DIR2)/%.cc, $(BUILD_DIR)/%.o, $(DRIVER2_SOURCES))
OBJS3 = $(patsubst %.cc, $(BUILD_DIR)/%.o, $(PROJECT))

##############
##  TARGET 	##
##############
all: create build

build: $(OBJS1) $(OBJS2) $(OBJS3)
	$(COMPILER_CALL) $(OBJS1) $(OBJS2) $(OBJS3) -o $(BUILD_DIR)/$(TARGET)

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
$(BUILD_DIR)/%.o: $(SOURCE_DIR1)/%.cc
	$(COMPILER_CALL) -c $< -o $@

$(BUILD_DIR)/%.o: $(SOURCE_DIR2)/%.cc
	$(COMPILER_CALL) -c $< -o $@

$(BUILD_DIR)/%.o: %.cc
	$(COMPILER_CALL) -c $< -o $@

##############
##  PHONY   ##
##############
.PHONY: build all create execute clean