OPT = /usr/local
HEAP_PTRS = 0
PLATFORMS = i86_64-fedora
# i86-redhat
# sparc-sol9
# i86-freebsd

ifeq ($PLATFORMS,i86_64-fedora)
MM=-m64
endif

all:
		cd doc; \
		mkdir -p man; \
		mkdir -p man/man1; \
		mkdir -p man/man3; \
		mkdir -p man/man5; \
		mkdir -p html; \
		mkdir -p html/man1; \
		mkdir -p html/man3; \
		mkdir -p html/man5; \
		gmake all ROOT=$(OPT); \
		cd ..; \
		cd libbloom-master; \
		gmake all MM=$(MM); \
		cd ..; \
		for PF in $(PLATFORMS);\
			do \
				cd $$PF; \
				mkdir -p bin; \
				mkdir -p lib; \
				gmake all ROOT=$(OPT) PTRS=$(HEAP_PTRS); \
				cd ..; \
			done

clean:
		cd doc; \
		gmake -i clean; \
		cd ..; \
		cd libbloom-master; \
		gmake -i clean; \
		cd ..; \
		for PF in $(PLATFORMS);\
			do cd $$PF; gmake -i clean; cd ..; done

install:
		cd doc; \
		gmake -i install ROOT=$(OPT); \
		cd ..; \
		cd libbloom-master; \
		gmake -i install ROOT=$(OPT); \
		cd ..; \
		for PF in $(PLATFORMS);\
			do cd $$PF; gmake -i install ROOT=$(OPT); cd ..; done

uninstall:		
		for PF in $(PLATFORMS); \
			do cd $$PF; gmake -i uninstall ROOT=$(OPT); cd ..; done
		cd libbloom-master; \
		gmake -i uninstall ROOT=$(OPT); cd ..
