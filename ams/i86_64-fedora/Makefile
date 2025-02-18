INCL = ../include
ICI_INCL = ../../ici/include
ICI_LIB = ../../ici/i86_64-fedora/lib
DGR_LIB = ../../dgr/i86_64-fedora/lib
BP_LIB = ../../bpv7/i86_64-fedora/lib
API = ../library
TEST = ../test
UTILS = ../utils
RAMS = ../rams

# OPT = -O -Dlinux
OPT = -g -Wall -Werror -Dlinux -DUDPTS -DTCPTS -DDGRTS -DNOEXPAT -fPIC -DSPACE_ORDER=3
CC = gcc $(OPT) $(ADD_FLAGS) -I$(API) -I$(INCL) -I$(RAMS) -I$(ROOT)/include -I$(ICI_INCL) -I../../dgr/include -I../../ici/library -I../../bpv7/include -I../../dgr/library -L$(ICI_LIB) -L$(BP_LIB) -L$(DGR_LIB) 
LDFLAGS = -fPIC -shared
LD = gcc $(LDFLAGS)

LIBAMSOBJS = \
	libams.o \
	amscommon.o \
	loadmib.o \
	crypt.o \
	dgrts.o \
	udpts.o \
	tcpts.o

AMSDOBJS = \
	amsd.o \
	libams.o \
	amscommon.o \
	loadmib.o \
	crypt.o \
	dgrts.o \
	udpts.o \
	tcpts.o

RAMSTESTOBJS = \
	librams.o \
	ramscommon.o \
	ramsgate.o

PUBINCLS = \
	$(INCL)/ams.h

LBP = -lbp

RUNTIMES = amsd amshello amsshell amslog amslogprt amsbenchs amsbenchr ramsgate amsstop amsmib

ALL = check libams.so $(RUNTIMES)

all:		$(ALL)

check:		$(PUBINCLS)
		rm -f *.o
		touch check
		mkdir -p ./lib/
		touch ./bin/

clean:
		rm -f *.o
		rm -f *.so
		rm -f $(ALL)
		rm -f ./lib/*
		rm -f ./bin/*

install:
		cp ../include/* $(ROOT)/include
		cp lib/* $(ROOT)/lib
		cp bin/* $(ROOT)/bin
		
uninstall:		
		rm $(ROOT)/lib/libams*
		rm $(ROOT)/include/ams*
		rm $(ROOT)/include/rams*
		rm $(ROOT)/bin/ams*
		rm $(ROOT)/bin/ramsgate	

#	-	-	Daemon executable	-	-	-	-

amsd:		$(AMSDOBJS) $(API)/amscommon.h
		$(CC) -o amsd $(AMSDOBJS) -L./lib -L$(ROOT)/lib -ldgr -lici -lpthread -lm
		cp amsd ./bin

#	-	-	Test executables	-	-	-	-

amshello:	amshello.o libams.so $(INCL)/ams.h
		$(CC) -o amshello amshello.o -L./lib -L$(ROOT)/lib -lams -ldgr -lici -lpthread -lm
		cp amshello ./bin

amsbenchs:	amsbenchs.o libams.so $(INCL)/ams.h
		$(CC) -o amsbenchs amsbenchs.o -L./lib -L$(ROOT)/lib -lams -ldgr -lici -lpthread -lm
		cp amsbenchs ./bin

amsbenchr:	amsbenchr.o libams.so $(INCL)/ams.h
		$(CC) -o amsbenchr amsbenchr.o -L./lib -L$(ROOT)/lib -lams -ldgr -lici -lpthread -lm
		cp amsbenchr ./bin

#	-	-	Utility executables	-	-	-	-

amsshell:	amsshell.o libams.so $(INCL)/ams.h
		$(CC) -o amsshell amsshell.o -L./lib -L$(ROOT)/lib -lams -ldgr -lici -lpthread -lm
		cp amsshell ./bin

amslog:		amslog.o libams.so $(INCL)/ams.h
		$(CC) -o amslog amslog.o -L./lib -L$(ROOT)/lib -lams -ldgr -lici -lpthread -lm
		cp amslog ./bin

amslogprt:	amslogprt.o
		$(CC) -o amslogprt amslogprt.o -L./lib -L$(ROOT)/lib
		cp amslogprt ./bin

amsstop:	amsstop.o libams.so $(INCL)/ams.h
		$(CC) -o amsstop amsstop.o -L./lib -L$(ROOT)/lib -lams -ldgr -lici -lpthread -lm
		cp amsstop ./bin

amsmib:		amsmib.o libams.so $(INCL)/ams.h
		$(CC) -o amsmib amsmib.o -L./lib -L$(ROOT)/lib -lams -ldgr -lici -lpthread -lm
		cp amsmib ./bin

#	-	-	RAMS executable		-	-	-	-

ramsgate:	$(RAMSTESTOBJS) $(RAMS)/rams.h $(RAMS)/ramscommon.h libams.so $(INCL)/ams.h
		$(CC) -o ramsgate $(RAMSTESTOBJS) -L./lib -L$(ROOT)/lib $(LBP) -lams -ldgr -lici -lpthread -lm 
		cp ramsgate ./bin

#	-	-	Libraries	-	-	-	-	-

libams.so:	$(LIBAMSOBJS) $(API)/amsP.h
		$(LD) -o libams.so $(LIBAMSOBJS)
		cp libams.so ./lib

#	-	-	Object modules	-	-	-	-	-

%.o:		$(API)/%.c
		$(CC) -c $<

%.o:		$(TEST)/%.c
		$(CC) -c $<

%.o:		$(UTILS)/%.c
		$(CC) -c $<

%.o:		$(RAMS)/%.c
		$(CC) -c $<
