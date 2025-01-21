#
# CDDL HEADER START
#
# The contents of this file are subject to the terms of the
# Common Development and Distribution License, Version 1.0 only
# (the "License").  You may not use this file except in compliance
# with the License.
#
# You can obtain a copy of the license at COPYING
# See the License for the specific language governing permissions
# and limitations under the License.
#
# When distributing Covered Code, include this CDDL HEADER in each
# file and include the License file at COPYING.
# If applicable, add the following below this CDDL HEADER, with the
# fields enclosed by brackets "[]" replaced with your own identifying
# information: Portions Copyright [yyyy] [name of copyright owner]
#
# CDDL HEADER END
#
# Copyright (c) 2012, Joyent, Inc.  All rights reserved.
# Copyright (c) 2025, Hans Rosenfeld
#

VER =	db-18.1.40

include ../Makefile.defs

BUILD64 =	yes
BUILD32 =	yes

SEPARATE_BUILD = yes

UNPACK_SENTINEL = dist/configure
AUTOCONF_CONFIGURE = $(UNPACK_SENTINEL)

CPPFLAGS += \
	-D_FILE_OFFSET_BITS=64 \
	-D_LARGEFILE_SOURCE

AUTOCONF_OPTS += \
	--enable-compat185

include ../Makefile.targ

all: all_autoconf

install: all
	DESTDIR=$(DESTDIR) VERS=$(OBJ.64) MACH64=/amd64 \
	    /bin/bash ./install-bdb
	DESTDIR=$(DESTDIR) VERS=$(OBJ.32) MACH64= \
	    /bin/bash ./install-bdb
