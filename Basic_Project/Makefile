TARGET = main
CXX = g++
CFLAG = -g
OBJS = main.o my_lib.o

build: $(OBJS)
	$(CXX) $(CFLAG) -o $(TARGET) $(OBJS)

main.o:
	g++ -c main.cc

my_lib.o:
	g++ -c my_lib.cc

execute:
	./main

clean:
	rm -f *~ *.o main