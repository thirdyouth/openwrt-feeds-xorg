# 
# Copyright (C) 2007 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# blogic@openwrt.org
include $(TOPDIR)/rules.mk

PKG_BASE_NAME:=encodings
PKG_NAME:=encodings
PKG_RELEASE:=2
PKG_VERSION:=1.0.2
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_BUILD_DIR=$(BUILD_DIR)/Xorg/$(_CATEGORY)/${PKG_NAME}-$(PKG_VERSION)/
PKG_SOURCE_URL:=http://xorg.freedesktop.org/releases/X11R7.3/src/font
PKG_MD5SUM:=11adda157b03d63fd61d95ad7ef00466

PKG_BUILD_DEPENDS:= font-util

include $(INCLUDE_DIR)/package.mk

define Package/encodings
  SECTION:=xorg-font
  CATEGORY:=Xorg
  SUBMENU:=font
  DEPENDS:= +xserver @DISPLAY_SUPPORT
  TITLE:=encodings
  URL:=http://xorg.freedesktop.org/
endef

define Build/InstallDev
	DESTDIR="$(1)" $(MAKE) -C $(PKG_BUILD_DIR) $(MAKE_FLAGS) install
endef

CONFIGURE_ARGS+=--disable-iso8859-2 --disable-iso8859-3 --disable-iso8859-4  --disable-iso8859-5 --disable-iso8859-7 --disable-iso8859-8 --disable-iso8859-9 --disable-iso8859-10 --disable-iso8859-11 --disable-iso8859-13 --disable-iso8859-14 --disable-iso8859-16 --disable-koi8-r --disable-jisx0201

define Build/Compile
	UTIL_DIR="$(STAGING_DIR)/usr/lib/X11/fonts/util/" make -e -C $(PKG_BUILD_DIR)
	DESTDIR=$(PKG_INSTALL_DIR) $(MAKE) -C $(PKG_BUILD_DIR) $(MAKE_FLAGS) install
	find $(PKG_INSTALL_DIR) -name fonts.dir | \
		xargs -i -t \
			sed -i '1d' {} 
	find $(PKG_INSTALL_DIR) -name fonts.dir | \
		xargs -i -t \
			mv {} {}.encodings
endef

define Package/encodings/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/* $(1)/usr/lib/
endef

define Package/encodings/postinst
#!/bin/sh

FILE_NEW=`find $${IPKG_INSTROOT} -name fonts.dir.encodings`
FILE_OLD=`dirname $${FILE_NEW}`/fonts.dir

echo found $${FILE}

if [ ! -z $${FILE_NEW} ]; then
	if [ -f $${FILE_OLD} ]; then
		sed -i "1d" $${FILE_OLD}
		cat $${FILE_NEW} >> $${FILE_OLD}
		rm -rf $${FILE_NEW}
		mv $${FILE_OLD} $${FILE_OLD}.tmp
	else
		mv $${FILE_NEW} $${FILE_OLD}.tmp
	fi
	(echo `wc -l $${FILE_OLD}.tmp | awk '{print($$1)}'`; cat $${FILE_OLD}.tmp) > $${FILE_OLD}
	rm $${FILE_OLD}.tmp
fi
endef

ifeq (encodings,font-util)
define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR)/ 
endef
endif

$(eval $(call BuildPackage,encodings))

