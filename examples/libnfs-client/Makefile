# name of your application
APPLICATION = libnfs-client

# If no BOARD is found in the environment, use this default:
BOARD ?= native

# This has to be the absolute path to the RIOT base directory:
RIOTBASE ?= $(CURDIR)/../..

USEMODULE += posix_inet
USEMODULE += posix_select

USEPKG += libnfs

# Comment this out to disable code in RIOT that does safety checking
# which is not needed in a production environment but helps in the
# development process:
DEVELHELP ?= 1

# Change this to 0 show compiler invocation lines by default:
QUIET ?= 1

CFLAGS += -DHAVE_NETINET_IN_H

include $(RIOTBASE)/Makefile.include
