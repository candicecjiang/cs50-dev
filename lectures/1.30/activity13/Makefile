#------------------------------------------
# technique for detecting operating system
# (Note: Requires gnumake)
#
PLATFORM := $(shell uname)
ifeq  ($(PLATFORM),Linux)
OS = linux
else
OS = not-linux
endif
#------------------------------------------
#
.PHONY: all, clean, whereami, release
CC=gcc
CFLAGS=-Wall -pedantic -std=c11 -ggdb
RELCFLAGS=-Wall -pedantic -std=c11
LIBOBJS=top.o middle.o bottom.o
#-----------------------------------
all:	whereami atest
release:  whereami clean
	$(CC) $(RELCFLAGS) -c top.c middle.c bottom.c atest.c
	ar -r act9.a $(LIBOBJS)
	$(CC) -o atest atest.o act9.a
atest:	atest.o act9.a
	@echo ======================
	@echo Building atest now ...
	$(CC) -o atest atest.o act9.a
	@echo ... finished!
atest.o: 	atest.c
top.o:	 	top.c
middle.o:	middle.c
bottom.o:	bottom.c	
act9.a:		$(LIBOBJS)
	ar -r $@  $^
whereami:
	@echo "********"
	@echo $(OS)
	@echo "********"
clean:
	-rm -f atest atest.o top.o middle.o bottom.o
	-rm -f act9.a