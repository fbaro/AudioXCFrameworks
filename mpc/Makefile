FRAMEWORK_NAME := mpc
XCODEPROJ := mpc.xcodeproj

xcframework: patch

include ../xcframework.mk

SRC_ARCHIVE := musepack_src_r475.tar.gz
SRC_DOWNLOAD_URL := https://files.musepack.net/source/$(SRC_ARCHIVE)
SRC_DIR := musepack-src
PATCH_FILES := angle_bracket_include.patch extern.patch vio.patch

$(SRC_ARCHIVE):
	curl $(SRC_DOWNLOAD_URL) -o $@

$(SRC_DIR):
	mkdir $(SRC_DIR) && tar -xf $(SRC_ARCHIVE) --directory $(SRC_DIR) --strip-components 1

download: $(SRC_ARCHIVE)
.PHONY: download

extract: download $(SRC_DIR)
.PHONY: extract

patch: extract $(PATCH_FILES:.patch=.patched)
.PHONY: patch

%.patched: %.patch
	if [ -e $@ ]; then patch -p0 -R < $@; fi
	patch -p0 < $<
	cp -f $< $@

realclean:: clean
	rm -f $(PATCH_FILES:.patch=.patched)
	rm -f $(SRC_ARCHIVE)
	rm -Rf $(SRC_DIR)
