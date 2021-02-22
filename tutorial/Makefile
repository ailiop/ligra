ifdef LONG
INTT = -DLONG
endif

ifdef EDGELONG
INTE = -DEDGELONG
endif

#compilers
ifdef OPENCILK
PCC = $(OPENCILK_DIR)/bin/clang++
PCFLAGS = -std=c++14 -fopencilk -O3 -DOPENCILK $(INTT) $(INTE)
PLFLAGS = -fopencilk

else ifdef CILKPLUS
PCC = g++
PCFLAGS = -fcilkplus -lcilkrts -O3 -DCILKP $(INTT) $(INTE)
PLFLAGS = -fcilkplus -lcilkrts

else ifdef MKLROOT
PCC = icpc
PCFLAGS = -O3 -DCILKP $(INTT) $(INTE)

else ifdef OPENMP
PCC = g++
PCFLAGS = -fopenmp -march=native -O3 -DOPENMP $(INTT) $(INTE)

else
PCC = g++
PCFLAGS = -O3 $(INTT) $(INTE)
endif

COMMON= ligra.h graph.h compressedVertex.h vertex.h utils.h IO.h parallel.h gettime.h quickSort.h parseCommandLine.h byte.h byteRLE.h nibble.h byte-pd.h byteRLE-pd.h nibble-pd.h vertexSubset.h encoder.C blockRadixSort.h transpose.h index_map.h maybe.h sequence.h edgeMap_utils.h binary_search.h

ALL= encoder BFS BellmanFord Components Radii KCore

all: $(ALL)

% : %.C $(COMMON)
	$(PCC) $(PCFLAGS) -o $@ $< 

$(COMMON):
	ln -s ../ligra/$@ .

.PHONY : clean

clean :
	rm -f *.o $(ALL)

cleansrc :
	rm -f *.o $(ALL)
	rm $(COMMON)
