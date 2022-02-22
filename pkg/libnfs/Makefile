PKG_NAME=libnfs
PKG_URL=https://github.com/larseggert/libnfs.git
PKG_VERSION=3089851e93dd30ee13b95b89b5fdacbf96ef02c2
PKG_LICENSE=CC-0

include $(RIOTBASE)/pkg/pkg.mk

all:
	mkdir -p $(BINDIR)/$(PKG_NAME)/rquota \
		 $(BINDIR)/$(PKG_NAME)/lib \
		 $(BINDIR)/$(PKG_NAME)/rquota \
		 $(BINDIR)/$(PKG_NAME)/portmap \
		 $(BINDIR)/$(PKG_NAME)/nfs \
		 $(BINDIR)/$(PKG_NAME)/mount
	$(QQ)"$(MAKE)" -C $(PKG_SOURCE_DIR) -f $(CURDIR)/Makefile.cifra


$(PKG_PATCHED): $(PKG_PATCHED_PREREQUISITES)
	touch $@
$(PKG_DOWNLOADED): $(MAKEFILE_LIST)
	true
