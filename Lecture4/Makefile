EXE_NAME := myROOTCommand
OBJECTS  := myROOTCommand.o

# Extract CXXFLAGS cleanly without extra -I prefix
CXXFLAGS := -std=c++17 -g -Wall $(shell root-config --cflags)
LDFLAGS  := -Wl
LDLIBS   := $(shell root-config --libs) -lvectorDict

.PHONY: all clean

all: $(EXE_NAME)

# Link executable
$(EXE_NAME): $(OBJECTS)
	g++ $(LDFLAGS) -g -Wall -o $@ $^ $(LDLIBS)

# Pattern rule for object files (.cpp source)
%.o: %.cpp
	g++ $(CXXFLAGS) -c $< -o $@

# Pattern rule for auto-generated dependencies (.d)
%.d: %.cpp
	g++ $(CXXFLAGS) -MM -MT '$*.o $@' $< -o $@

-include $(OBJECTS:.o=.d)

clean:
	rm -f *.o *.d *~ \#* $(EXE_NAME)
