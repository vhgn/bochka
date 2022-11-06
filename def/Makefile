name = lib$(shell cat Bochkapkg).a

headers = $(wildcard *.h)
objects = $(patsubst %.c,%.o,$(wildcard *.c))
libraries = $(patsubst lib%.a,-l%,$(wildcard lib/*))
flags = -Wall $(libraries)

lib: $(name)

$(name): $(objects)
	ar -rc $@ $^
	ranlib $@

%.o: %.c $(headers)
	gcc $< -c -o $@ $(flags)

clean:
	rm -f $(objects) $(library)

.PHONY: clean
