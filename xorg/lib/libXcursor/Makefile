#
# Copyright (C) 2007-2019 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# blogic@openwrt.org

include $(TOPDIR)/rules.mk

PKG_NAME:=libXcursor
PKG_RELEASE:=2
PKG_VERSION:=1.1.14

PKG_SOURCE_URL:=http://xorg.freedesktop.org/releases/individual/lib/
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_BUILD_DIR:=$(BUILD_DIR)/Xorg/$(PKG_NAME)-$(PKG_VERSION)/
PKG_HASH:=9bc6acb21ca14da51bda5bc912c8955bc6e5e433f0ab00c5e8bef842596c33df

PKG_FIXUP:=libtool
PKG_INSTALL:=1
PKG_BUILD_DEPENDS:=fixesproto

include $(INCLUDE_DIR)/package.mk

define Package/libXcursor
  SECTION:=xorg-libraries
  CATEGORY:=Xorg
  SUBMENU:=libraries
  DEPENDS:=+libXrender +libXfixes +libX11
  TITLE:=libXcursor
  URL:=http://xorg.freedesktop.org/
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/{lib/pkgconfig,include/X11/Xcursor}
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/*.{so*,a,la} \
		$(1)/usr/lib/
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/lib/pkgconfig/* \
		$(1)/usr/lib/pkgconfig/
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/include/X11/Xcursor/* \
		$(1)/usr/include/X11/Xcursor
endef

define Package/libXcursor/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/*.so* \
		$(1)/usr/lib/
endef

$(eval $(call BuildPackage,libXcursor))
