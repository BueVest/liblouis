CC := gcc
DISPLAY_NAMES_FILE := display-names

export LOUIS_TABLEPATH = $(CURDIR)/../../tables
export GOPATH = $(CURDIR)/.go-packages

.PHONY : check
check : generate ../../tables/nl-NL-g0.utb
	./$< $(DISPLAY_NAMES_FILE) >$<.log 2>$<.log

generate : generate.o displayLanguage.a ../../liblouis/liblouis.la
	../../libtool --tag=CC --mode=link $(CC) -o $@ $^ -lpthread

generate.o : generate.c displayLanguage.h
	$(CC) -I. -I../../liblouis -g -O2 -c -o $@ $<

displayLanguage.a displayLanguage.h : displayLanguage.go
	go build -buildmode=c-archive $<

../../tables/nl-NL-g0.utb :
	$(MAKE) -C $(dir $@) $(notdir $@)

.PHONY : clean
clean :
	rm -rf displayLanguage.a displayLanguage.h $(GOPATH) generate.o generate generate.log
