############################################################
#
# Esempio di Makefile usato per il corso 
# Programmazione avanzata per il calcolo scientifico
# Da modificare a seconda dei casi 
#
############################################################
#
# Nella variabile d'ambiente PACS_ROOT e` contenuta la directory di base 
# dove sono messe le utilities (librerie e include files) usati nel corso e
# non presenti nel folder dove si sta lavorando. 
# Se non e` settata si considera un valore di default (/usr/local)
#
ifeq ($(PACS_ROOT),)
ROOT=/usr/local
else
ROOT=$(PACS_ROOT)
endif
#
# Il compilatore c++ usato
#
CXX = g++ 
# Make usa la variabile CC anche per indicare il loader.
# Per semplicita la metto pari a CXX 
# 
CC =$(CXX)

OPTFLAGS = -g -Wall
# -c       compile only, generate corresponding .o files
# -g       generate code suitable for the debugger
# -p       generate code suitable for the profiler
# -O       attemp code optimizations

# where to look for include files
INCLS  = -I. -I.. 

CXXFLAGS=$(OPTFLAGS)
#
# Flags per il preprocessore
# 
CPPFLAGS= $(INCLS)

#
# Nome del file che viene incluso e contiene le dipendenze
# dagli headers autogenerate 
#
DEPEND=make.dep

SRCS=numerical_integration.cpp numerical_rule.cpp
# get the corresponding object file
OBJS = $(SRCS:.cpp=.o)
# get all headers in the working directory
HEADERS=$(SRCS:.cpp=.hpp)

# Additional libraries
#LIBS = -lm                   # for math library
LDLIBS =-lm 

# In questo corso, per semplicita`, gli eseguibili vengono sempre chiamati
# 'main*.cpp' chiaramente non e` obbligatorio (ne consigliabile in
# generale)!  Si assume anche che ce ne sia solo uno per directory
#
ALLSRC=$(wildcard *.cpp)
EXESRCS=$(filter main%.cpp,$(ALLSRC))
EXEC=$(EXESRCS:.cpp=)
EXEOBJS=$(EXESRCS:.cpp=.o)
#
LIBNAME=libnumint.a
#
LIBOBJS=$(LIBNAME)($(OBJS))
#
# Aggiungere la nostra libreria
LDLIBS += -L. -lnumint

#========================== ORA LA DEFINIZIONE DEGLI OBIETTIVI
.phony= all  clean doc

all: $(DEPEND) $(LIBNAME) $(EXEC)

doc:
	doxygen

clean:
	\rm -f $(EXEC) $(OBJS) $(LIBNAME) $(DEPEND) $(EXEOBJS)
	\rm -r -f doc
# Assumiamo che i MAIN dipendono da tutti i *.o e da tutti gli header nella
# directory corrente
# Questo e` vero nei casi piu` semplici. Altrimenti si modifichi di volta in volta 
# a seconda del caso

$(LIBNAME): $(LIBOBJS)

$(DEPEND): $(SRCS) $(EXESRCS)
	g++ $(CPPFLAGS) -MM $(SRCS) $(EXESRCS) -MF $(DEPEND)

-include $(DEPEND)




