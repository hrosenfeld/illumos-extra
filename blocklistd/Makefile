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

VER =	blocklist-5413de523fa99fc805c632aee0d5f20b3cbb621e

include ../Makefile.defs

BUILD64 =	yes
BUILD32 =	yes

OBJ.64 = $(VER.64)/port
OBJ.32 = $(VER.32)/port

UNPACK_SENTINEL = port/configure.ac
AUTOCONF_CONFIGURE = configure

include ../Makefile.targ

AUTOCONF_ENV += \
	DESTDIR="$(DESTDIR)"

AUTOCONF_OPTS.64 += --libdir=$(AUTOCONF_PREFIX)/lib/amd64
AUTOCONF_OPTS.32 += --libdir=$(AUTOCONF_PREFIX)/lib
AUTOCONF_OPTS += --libexecdir=$(AUTOCONF_PREFIX)/lib/blocklistd
AUTOCONF_OPTS += --localstatedir=/var
AUTOCONF_OPTS += --sysconfdir=/etc

$(OBJ.64)/$(AUTOCONF_CONFIGURE): $(VER.64)/$(UNPACK_SENTINEL)
	(cd $(OBJ.64) && env - PATH=$(PATH) $(AUTOCONF_ENV) aclocal)
	(cd $(OBJ.64) && env - PATH=$(PATH) $(AUTOCONF_ENV) autoreconf -fi)

$(OBJ.32)/$(AUTOCONF_CONFIGURE): $(VER.32)/$(UNPACK_SENTINEL)
	(cd $(OBJ.32) && env - PATH=$(PATH) $(AUTOCONF_ENV) aclocal)
	(cd $(OBJ.32) && env - PATH=$(PATH) $(AUTOCONF_ENV) autoreconf -fi)

$(VER.64)/$(AUTOCONF_CONFIGURE): $(OBJ.64)/$(AUTOCONF_CONFIGURE)
	cp $< $@

$(VER.32)/$(AUTOCONF_CONFIGURE): $(OBJ.32)/$(AUTOCONF_CONFIGURE)
	cp $< $@

all: all_autoconf

install: all install_autoconf
	DESTDIR=$(DESTDIR) /bin/bash ./install-blocklistd
