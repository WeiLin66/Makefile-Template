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
	echo $(COMPILER_CALL) # print g++ command
	$(COMPILER_CALL) $(LDFLAGS) -o $(TARGET) $(OBJS)

main.o:
	$(COMPILER_CALL) -c main.cc

my_lib.o:
	$(COMPILER_CALL) -c my_lib.cc

execute:
	./main

clean:
	rm -f *~ *.o main