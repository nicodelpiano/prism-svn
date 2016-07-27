################################################
#  NB: This Makefile is designed to be called  #
#      from the main PRISM Makefile. It won't  #
#      work on its own because it needs        #
#      various options to be passed in         #
################################################

default: all

all: checks ../../lib/glpk

# Try and prevent accidental makes (i.e. called manually, not from top-level Makefile)
checks:
	@if [ "$(LIBSUFFIX)" = "" ]; then \
	  (echo "Error: This Makefile is designed to be called from the main PRISM Makefile"; exit 1) \
	fi; 

../../lib/glpk:
	@(if [ "$(OSTYPE)" = "cygwin" ]; then \
	  cp bin/$(BINDISTSUFFIX)/glpk-java.jar ../../lib; \
	  cp bin/$(BINDISTSUFFIX)/$(LIBPREFIX)glpk$(LIBSUFFIX) ../../lib; \
	else \
	  (cd src/glpk && \
           CPP=$(gcc -E) LD="" && \
           ./configure --with-gmp && \
           make \
	  ) && cp --remove-destination src/glpk/src/.libs/$(LIBPREFIX)glpk$(LIBSUFFIX).40 ../../lib/; \
	  cp --remove-destination src/glpk/src/.libs/$(LIBPREFIX)glpk$(LIBSUFFIX) ../../lib/; \
	fi)

clean: checks
	rm -f lib/$(LIBPREFIX)glpk$(LIBSUFFIX) ../../lib/$(LIBPREFIX)glpk$(LIBSUFFIX).40

celan:	clean

#################################################
