
C_SRC_OUTPUT = ../priv/eblas.so

ERL_INCLUDE_DIR = $(ERLANG_ROOT_DIR)/usr/include

UNAME_SYS := $(shell uname -s)
ifeq ($(UNAME_SYS), Darwin)
	CC ?= cc
	CFLAGS := -O3 -std=c99 -arch x86_64 -flat_namespace -undefined suppress -finline-functions -Wall -Wmissing-prototypes
else ifeq ($(UNAME_SYS), FreeBSD)
	CC ?= cc
	CFLAGS := -O3 -std=c99 -finline-functions -Wall -Wmissing-prototypes
else ifeq ($(UNAME_SYS), Linux)
	CC ?= gcc
	CFLAGS := -O3 -std=c99 -finline-functions -Wall -Wmissing-prototypes
endif

DISTRO_NAME = $(shell lsb_release -si)
ifeq ($(DISTRO_NAME), CentOS)
	CFLAGS := $(CFLAGS) $(shell pkg-config --cflags cblas blas atlas)
	LIBS := $(LIBS) $(shell pkg-config --libs cblas blas atlas)
else ifeq ($(DISTRO_NAME), Fedora)
	CFLAGS := $(CFLAGS) $(shell pkg-config --cflags cblas blas atlas)
	LIBS := $(LIBS) $(shell pkg-config --libs cblas blas atlas)
else ifeq ($(DISTRO_NAME), Arch)
	CFLAGS := $(CFLAGS) $(shell pkg-config --cflags cblas blas)
	LIBS := $(LIBS) $(shell pkg-config --libs cblas blas)
# Debian and Ubuntu
else
	CFLAGS := $(CFLAGS) $(shell pkg-config --cflags blas-atlas)
	LIBS := $(LIBS) $(shell pkg-config --libs blas-atlas)
endif

$(C_SRC_OUTPUT): *.c
	$(CC) $(CFLAGS) *.c -g -fPIC -shared -o $(C_SRC_OUTPUT) -I $(ERL_INCLUDE_DIR) \
		$(C_SRC_OPTS) $(LIBS)

clean:
	rm -f $(C_SRC_OUTPUT)
	rm -f *.o
	rm -f *~
