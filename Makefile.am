# Copyright (c) 2000-2011 Apple Inc. All Rights Reserved.
#
# This file contains Original Code and/or Modifications of Original Code
# as defined in and that are subject to the Apple Public Source License
# Version 2.0 (the 'License'). You may not use this file except in
# compliance with the License. Please obtain a copy of the License at
# http://www.opensource.apple.com/apsl/ and read it before using this
# file.
# 
# The Original Code and all software distributed under the License are
# distributed on an 'AS IS' basis, WITHOUT WARRANTY OF ANY KIND, EITHER
# EXPRESS OR IMPLIED, AND APPLE HEREBY DISCLAIMS ALL SUCH WARRANTIES,
# INCLUDING WITHOUT LIMITATION, ANY WARRANTIES OF MERCHANTABILITY,
# FITNESS FOR A PARTICULAR PURPOSE, QUIET ENJOYMENT OR NON-INFRINGEMENT.
# Please see the License for the specific language governing rights and
# limitations under the License.
# 

ACLOCAL_AMFLAGS = -I m4 --install

MODULE_NAME = mod_hfs_apple
MODULE_SRC2 = $(MODULE_NAME)2.c
MODULE = $(MODULE_NAME).so
OTHER_SRC = APPLE_LICENSE
APXS2=@APXS@
SRCFILES = Makefile $(MODULE_SRC) $(MODULE_SRC2) $(OTHER_SRC) $(HEADERS)
INSTALLDIR2 := $(shell $(APXS2) -q LIBEXECDIR)

MORE_FLAGS = -Wc,"$(RC_CFLAGS) -Wall -Wextra -Os -g"
MORE_FLAGS += -Wl,"$(RC_CFLAGS)"

MAKEFILEPATH = @DEVELOPER_DIR@/Makefiles
MAKEFILEDIR = $(MAKEFILEPATH)/pb_makefiles
include $(MAKEFILEDIR)/platform.make
include $(MAKEFILEDIR)/commands-$(OS).make

all: build
build $(MODULE): $(MODULE_SRC) $(OTHER_SRC)
	$(APXS2) -c $(MORE_FLAGS) -o $(MODULE) $(MODULE_SRC2) $(OTHER_SRC)
 
installsrc:
	@echo "Installing source files..."
	-$(RM) -rf $(SRCROOT)$(SRCPATH)
	$(MKDIRS) $(SRCROOT)$(SRCPATH)
	$(TAR) cf - $(SRCFILES) | (cd $(SRCROOT)$(SRCPATH) && $(TAR) xf -)

installhdrs:
	@echo "Installing header files..."

install-exec-local: $(MODULE)
	@echo "Installing Apache 2.2 module..."
	$(MKDIRS) $(SYMROOT)$(INSTALLDIR2)
	$(CP) .libs/$(MODULE) $(SYMROOT)$(INSTALLDIR2)
	$(CHMOD) 755 $(SYMROOT)$(INSTALLDIR2)/$(MODULE)
	$(MKDIRS) $(DSTROOT)$(INSTALLDIR2)
	$(STRIP) -x $(SYMROOT)$(INSTALLDIR2)/$(MODULE) -o $(DSTROOT)$(INSTALLDIR2)/$(MODULE)

clean-local:
	@echo "== Cleaning $(MODULE_NAME) =="
	-$(RM) -r -f .libs *.la *.lo *.slo *.o *~ *.cache || rmdir autom4te.cache

check-local: $(MODULE)
	@echo "MODULE is $(MODULE)"
	if test -e $(MODULE); then \
	  stat $(MODULE) && du $(MODULE); \
	elif test -d .libs && test -r .libs; then \
	  stat .libs/$(MODULE) && du .libs/$(MODULE); \
	elif test -x "`which find`"; then \
	  find . -name $(MODULE) -print; \
	fi
