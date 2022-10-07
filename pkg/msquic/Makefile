PKG_NAME    = msquic
# PKG_URL     = https://github.com/microsoft/msquic
# PKG_VERSION = main
PKG_URL     = https://github.com/larseggert/msquic.git
PKG_VERSION = riot
PKG_LICENSE = MIT

include $(RIOTBASE)/pkg/pkg.mk

.PHONY: ..cmake_version_supported
.PHONY: $(TOOLCHAIN_FILE)

CMAKE_MINIMAL_VERSION = 3.16

# REMOVE_CFLAGS =-Werror -fshort-enums
CFLAGS := $(filter-out $(REMOVE_CFLAGS), $(CFLAGS)) $(INCLUDES)

TOOLCHAIN_FILE = $(PKG_SOURCE_DIR)/xcompile-toolchain.cmake

all: $(BINDIR)/libmsquic.a

# BUILD_TYPE = MinSizeRel
BUILD_TYPE = Debug

$(TOOLCHAIN_FILE): FORCE
	$(RIOTTOOLS)/cmake/generate-xcompile-toolchain.sh > $(TOOLCHAIN_FILE)

$(PKG_BUILD_DIR)/Makefile: $(PKG_PREPARED) $(TOOLCHAIN_FILE) | ..cmake_version_supported
	cmake -B$(PKG_BUILD_DIR) -H$(PKG_SOURCE_DIR) \
		-DQUIC_BUILD_TOOLS=OFF -DQUIC_BUILD_TEST=OFF \
		-DQUIC_BUILD_PERF=OFF -DQUIC_BUILD_SHARED=OFF \
		-DQUIC_ENABLE_LOGGING=ON \
		-DCMAKE_TOOLCHAIN_FILE=$(TOOLCHAIN_FILE) \
		-DCMAKE_BUILD_TYPE=$(BUILD_TYPE) \
		-DRIOT=ON

$(PKG_BUILD_DIR)/bin/$(BUILD_TYPE)/libmsquic.a: $(PKG_BUILD_DIR)/Makefile
	cmake --build $(PKG_BUILD_DIR) --target msquic_lib -v

$(BINDIR)/libmsquic.a: $(PKG_BUILD_DIR)/bin/$(BUILD_TYPE)/libmsquic.a
	cmake --install $(PKG_BUILD_DIR) --prefix $(BINDIR)
	cp $(PKG_BUILD_DIR)/bin/$(BUILD_TYPE)/libmsquic.a $(BINDIR)/libmsquic.a

..cmake_version_supported:
	@ # Remove '-rcX' from version as they are not well handled
	$(Q)\
	CMAKE_VERSION=$$(cmake --version | sed -n '1 {s/cmake version //;s/-rc.*//;p;}'); \
	$(RIOTTOOLS)/has_minimal_version/has_minimal_version.sh "$${CMAKE_VERSION}" "$(CMAKE_MINIMAL_VERSION)" cmake

# to avoid clobbering local msquic source changes:
$(PKG_PATCHED): $(PKG_PATCHED_PREREQUISITES)
	touch $@
$(PKG_DOWNLOADED): $(MAKEFILE_LIST)
	true
