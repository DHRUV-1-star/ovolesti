##
## Makefile for ovolesti oct-file bindings.
##
## Assumes dependencies have been fetched into volesti/external/_deps/
## via tools/fetch_deps.sh.  All include paths are fixed — no detection,
## no branching.  The package installs offline from a tarball that
## includes the pre-populated _deps/ directory.
##
## Usage:
##   make                  # build all oct-files
##   make clean            # remove built artifacts
##

MKOCTFILE ?= mkoctfile

VOLESTI_DIR = volesti
DEPS_DIR    = $(VOLESTI_DIR)/external/_deps
EXT_DIR     = $(VOLESTI_DIR)/external

# --- Fixed include paths (all vendored) ---
EIGEN_FLAGS    = -I$(DEPS_DIR)/eigen-src
BOOST_FLAGS    = -I$(DEPS_DIR)/boost-src
SPECTRA_FLAGS  = -I$(DEPS_DIR)/spectra-src/include
VOLESTI_FLAGS  = -I$(VOLESTI_DIR)/include
# Bundled external headers (shipped with volesti, not fetched).
# Includes use paths like "PackedCSparse/PackedChol.h" or
# <minimum_ellipsoid/khach.h>, so the external/ directory itself
# must be on the include path.
BUNDLED_FLAGS  = -I$(EXT_DIR) -I$(EXT_DIR)/arpack++/include

# --- Compiler flags ---
CXXFLAGS = -std=c++17 -O2 -DDISABLE_LPSOLVE \
           $(EIGEN_FLAGS) $(BOOST_FLAGS) $(SPECTRA_FLAGS) \
           $(VOLESTI_FLAGS) $(BUNDLED_FLAGS)

# --- Oct-file targets ---
OCT_FILES = __volesti_HPolytope__.oct

.PHONY: all clean

all: $(OCT_FILES)

%.oct: %.cc
	$(MKOCTFILE) $(CXXFLAGS) $< -o $@

clean:
	rm -f *.oct *.o
