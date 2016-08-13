################################################
#  NB: This Makefile is designed to be called  #
#      from the main PRISM Makefile. It won't  #
#      work on its own because it needs        #
#      various options to be passed in         #
################################################

default: all

all: checks ../../lib/glpk

glpkvers = "4.60"

ALREADY_DOWNLOADED = $(shell ls src | grep glpk-$(glpkvers).tar.gz 2> /dev/null)
ALREADY_INSTALLED_LIB = $(shell find src/glpk/src/.libs -name $(LIBPREFIX)glpk$(LIBSUFFIX).40 2> /dev/null)
ALREADY_INSTALLED = 1

ifeq ($(ALREADY_INSTALLED_LIB),)
	ALREADY_INSTALLED = 0
endif

# Try and prevent accidental makes (i.e. called manually, not from top-level Makefile)
checks:
	@if [ "$(LIBSUFFIX)" = "" ]; then \
	  (echo "Error: This Makefile is designed to be called from the main PRISM Makefile"; exit 1) \
	fi; 

../../lib/glpk:
	@(if [ "$(OSTYPE)" != "cygwin" ]; then \
	  (mkdir src/ && cd src/ && \
	   (if [ "$(ALREADY_DOWNLOADED)" = "" ]; then \
	    wget http://ftp.gnu.org/gnu/glpk/glpk-$(glpkvers).tar.gz && \
	    tar -xzf glpk-$(glpkvers).tar.gz && \
	    mv glpk-$(glpkvers) glpk; \
	   fi) && \
	   cd glpk/ && \
	   (if [ $(ALREADY_INSTALLED) = 0 ]; then \
	    patch -p1 < ../../glpk_exact_solutions.patch && \
	    ./autogen.sh > /dev/null && \
            ./configure --with-gmp > /dev/null && \
            make; \
	   fi) \
	  ) && cp --remove-destination src/glpk/src/.libs/$(LIBPREFIX)glpk$(LIBSUFFIX).40 ../../lib/; \
	fi)

clean: checks
	rm -f ../../lib/$(LIBPREFIX)glpk$(LIBSUFFIX)
	rm -f ../../lib/$(LIBPREFIX)glpk$(LIBSUFFIX).40
	rm -rf src/*

celan:	clean

#################################################
