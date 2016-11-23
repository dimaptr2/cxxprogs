CC=g++
NAME=saploader
PREFLAGS=-I/usr/sap/nwrfcsdk/include -DNDEBUG -D_LARGEFILE_SOURCE -D_FILE_OFFSET_BITS=64 -DSAPonUNIX -DSAPwithUNICODE -D__NO_MATH_INLINES -DSAPwithTHREADS -DSAPonLIN -E
CXXFLAGS=-I/usr/sap/nwrfcsdk/include -std=c++11 -O2 -minline-all-stringops -g -fno-strict-aliasing -fno-omit-frame-pointer -m64 -fexceptions -funsigned-char -Wall -Wno-uninitialized -Wno-long-long -Wcast-align -pthread -fPIC -c
LDFLAGS=-L/usr/sap/nwrfcsdk/lib -O2 -minline-all-stringops -g -fno-strict-aliasing -fno-omit-frame-pointer  -m64 -fexceptions -funsigned-char -Wall -Wno-uninitialized -Wno-long-long -Wcast-align -pthread -fPIC

$(NAME): main.o saploader.o
	$(CC) $(LDFLAGS) -o $(NAME) main.o saploader.o -lsapnwrfc
	
main.o: main.i
	$(CC) $(CXXFLAGS) main.i
	
saploader.o: saploader.i
	$(CC) $(CXXFLAGS) saploader.i
	
precompile: src/main.cpp src/saploader.cpp
	$(CC) $(PREFLAGS) src/main.cpp > main.ii
	/usr/bin/perl u16lit.pl -cpp main.ii
	$(CC) $(PREFLAGS) src/saploader.cpp > saploader.ii
	/usr/bin/perl u16lit.pl -cpp saploader.ii

install: $(NAME)
	mv $(NAME) bin/
	
clean: *.o *.i *.ii
	rm -rf *.o *.i *.ii
