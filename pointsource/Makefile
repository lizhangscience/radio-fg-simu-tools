#
# Makefile for pointsource simulation tools
#
# Aaron LI
# 2015/04/15
#

CXX=		g++
CXXFLAGS=	-Og -Wall

FIO_LIBS=	-lfio -lcfitsio
TRNG_LIBS=	-ltrng4

FIO_PATH=	../fio
FIO_INC=	-I$(FIO_PATH)/include
FIO_LIBS=	-L$(FIO_PATH)/lib -lfio -lcfitsio
FIO_LDFLAGS=	-Wl,-rpath='$$ORIGIN/$(FIO_PATH)/lib'

TARGETS=	make_ptr_map create_gps_map simulate_gps
#TARGETS+=	simulate_gps_trng

all: $(TARGETS)

make_ptr_map: make_ptr_map.cc
	$(CXX) $(CXXFLAGS) -o $@ $< -lCCfits -lcfitsio

create_gps_map: create_gps_map.o
	$(CXX) $(CXXFLAGS) $(FIO_LDFLAGS) $(FIO_LIBS) -o $@ $<

simulate_gps: simulate_gps.o coscalc.o
	$(CXX) $(CXXFLAGS) -o $@ $^

simulate_gps.o: simulate_gps.cc coscalc.h
	$(CXX) $(CXXFLAGS) -c $<

simulate_gps_trng: simulate_gps_trng.o coscalc.o
	$(CXX) $(CXXFLAGS) $(TRNG_LIBS) -o $@ $^

simulate_gps_trng.o: simulate_gps_trng.cpp coscalc.h
	$(CXX) $(CXXFLAGS) -c $<

coscalc.o: coscalc.cc coscalc.h adapt_trapezoid.h
	$(CXX) $(CXXFLAGS) -c $<

%.o: %.cc
	$(CXX) $(CXXFLAGS) $(FIO_INC) -c $<


clean:
	-rm -f *.o *~ $(TARGETS)

