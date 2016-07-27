################################################
#  NB: This Makefile is designed to be called  #
#      from the main PRISM Makefile. It won't  #
#      work on its own because it needs        #
#      various options to be passed in         #
################################################

default: all

all: checks ../../lib/glpk_java

# Try and prevent accidental makes (i.e. called manually, not from top-level Makefile)
checks:
	@if [ "$(LIBSUFFIX)" = "" ]; then \
	  (echo "Error: This Makefile is designed to be called from the main PRISM Makefile"; exit 1) \
	fi; 

../../lib/glpk_java:
	@(if [ "$(OSTYPE)" != "cygwin" ]; then \
	  (cd src/glpk_java && \
           ./configure && \
           make \
	  ) && cp --remove-destination src/glpk_java/swig/glpk-java.jar ../../lib/; \
	  cp --remove-destination src/glpk_java/swig/.libs/$(LIBPREFIX)glpk_java$(LIBSUFFIX) ../../lib/; \
	fi)

clean: checks
	rm -f lib/$(LIBPREFIX)glpk_java$(LIBSUFFIX) ../../lib/glpk-java.jar

celan:	clean

#################################################
