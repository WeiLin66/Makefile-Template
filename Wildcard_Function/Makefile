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

TARGET = main

DEBUG = 0 # make build DEBUG=1 to enable GDB

CXX_STANDARD = c++20 # make build CXX_STANDARD=c++(version)
CXX = g++
CC = gcc
CXXFLAGS = -Wall -Wextra -std=$(CXX_STANDARD)
LDFLAGS = -lm

# if-else condition
ifeq ($(DEBUG), 1)
CXXFLAGS += -g -O0
else
CXXFLAGS += -O3 
endif

COMPILER_CALL = $(CXX) $(CXXFLAGS)

OBJS = main.o my_lib.o

build: $(OBJS)
	echo $(COMPILER_CALL)
	$(COMPILER_CALL) $(LDFLAGS) -o $(TARGET) $(OBJS)

##############
## PATTERNS ##
##############
# $@: the file name of the target
# $<: the name of the first dependency
# $^: the names of all prerequisites
%.o: %.cc
	$(COMPILER_CALL) -c $< -o $@

execute:
	./main

clean:
	rm -f *~ *.o main