# Copyright © 2012 Intel Corporation
#
# Permission is hereby granted, free of charge, to any person obtaining a
# copy of this software and associated documentation files (the "Software"),
# to deal in the Software without restriction, including without limitation
# the rights to use, copy, modify, merge, publish, distribute, sublicense,
# and/or sell copies of the Software, and to permit persons to whom the
# Software is furnished to do so, subject to the following conditions:
#
# The above copyright notice and this permission notice (including the next
# paragraph) shall be included in all copies or substantial portions of the
# Software.
#
# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
# EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
# MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND
# NONINFRINGEMENT.  IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT
# HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY,
# WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
# OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER
# DEALINGS IN THE SOFTWARE.

include $(top_srcdir)/src/gallium/Automake.inc

AM_CPPFLAGS = \
	-I$(top_srcdir)/include \
	-I$(top_srcdir)/src/gallium/state_trackers/xa \
	-I$(top_srcdir)/src/gallium/winsys

AM_CFLAGS = \
	$(GALLIUM_CFLAGS) \
	$(LIBUDEV_CFLAGS) \
	$(LIBDRM_CFLAGS)

pkgconfigdir = $(libdir)/pkgconfig
pkgconfig_DATA = xatracker.pc

lib_LTLIBRARIES = libxatracker.la

libxatracker_la_SOURCES =

libxatracker_la_LIBADD = \
	$(GALLIUM_PIPE_LOADER_LIBS) \
	$(top_builddir)/src/gallium/auxiliary/pipe-loader/libpipe_loader.la \
	$(top_builddir)/src/gallium/winsys/sw/null/libws_null.la \
	$(top_builddir)/src/gallium/state_trackers/xa/libxatracker.la \
	$(top_builddir)/src/gallium/auxiliary/libgallium.la \
	$(LIBUDEV_LIBS) \
	$(LIBDRM_LIBS)

libxatracker_la_LDFLAGS = \
	-no-undefined \
	-version-number $(XA_MAJOR):$(XA_MINOR):$(XA_TINY)

# FIXME: this shouldn't be needed
if HAVE_MESA_LLVM
# Mention a dummy pure C++ file to trigger generation of the $(LINK) variable
nodist_EXTRA_libxatracker_la_SOURCES = dummy-cpp.cpp

libxatracker_la_LIBADD += $(LLVM_LIBS)
libxatracker_la_LDFLAGS += $(LLVM_LDFLAGS)
else
# Mention a dummy pure C file to trigger generation of the $(LINK) variable
nodist_EXTRA_libxatracker_la_SOURCES = dummy-c.c
endif

include $(top_srcdir)/install-lib-links.mk