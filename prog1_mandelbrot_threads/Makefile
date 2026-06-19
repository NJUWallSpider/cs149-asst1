
CXX=g++ -m64
CXXFLAGS=-I../common -Iobjs/ -O3 -std=c++11 -Wall -fPIC
DEBUG_CXXFLAGS=-I../common -Iobjs_debug/ -O0 -g -std=c++11 -Wall -fPIC

APP_NAME=mandelbrot
DEBUG_APP_NAME=mandelbrot_debug
OBJDIR=objs
DEBUG_OBJDIR=objs_debug
COMMONDIR=../common

PPM_CXX=$(COMMONDIR)/ppm.cpp
PPM_OBJ=$(addprefix $(OBJDIR)/, $(subst $(COMMONDIR)/,, $(PPM_CXX:.cpp=.o)))
DEBUG_PPM_OBJ=$(addprefix $(DEBUG_OBJDIR)/, $(subst $(COMMONDIR)/,, $(PPM_CXX:.cpp=.o)))


default: $(APP_NAME)

.PHONY: default debug dirs debug_dirs clean

debug: $(DEBUG_APP_NAME)

dirs:
		/bin/mkdir -p $(OBJDIR)/

debug_dirs:
		/bin/mkdir -p $(DEBUG_OBJDIR)/

clean:
		/bin/rm -rf $(OBJDIR) $(DEBUG_OBJDIR) *.ppm *~ $(APP_NAME) $(DEBUG_APP_NAME)

OBJS=$(OBJDIR)/main.o $(OBJDIR)/mandelbrotSerial.o $(OBJDIR)/mandelbrotThread.o $(PPM_OBJ)
DEBUG_OBJS=$(DEBUG_OBJDIR)/main.o $(DEBUG_OBJDIR)/mandelbrotSerial.o $(DEBUG_OBJDIR)/mandelbrotThread.o $(DEBUG_PPM_OBJ)

$(APP_NAME): dirs $(OBJS)
		$(CXX) $(CXXFLAGS) -o $@ $(OBJS) -lm -lpthread

$(DEBUG_APP_NAME): debug_dirs $(DEBUG_OBJS)
		$(CXX) $(DEBUG_CXXFLAGS) -o $@ $(DEBUG_OBJS) -lm -lpthread

$(OBJDIR)/%.o: %.cpp
		$(CXX) $< $(CXXFLAGS) -c -o $@

$(OBJDIR)/%.o: $(COMMONDIR)/%.cpp
	$(CXX) $< $(CXXFLAGS) -c -o $@

$(DEBUG_OBJDIR)/%.o: %.cpp
		$(CXX) $< $(DEBUG_CXXFLAGS) -c -o $@

$(DEBUG_OBJDIR)/%.o: $(COMMONDIR)/%.cpp
	$(CXX) $< $(DEBUG_CXXFLAGS) -c -o $@

$(OBJDIR)/main.o: $(COMMONDIR)/CycleTimer.h

$(DEBUG_OBJDIR)/main.o: $(COMMONDIR)/CycleTimer.h
