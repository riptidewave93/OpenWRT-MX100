#
# Copyright (C) 2021 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=nu801
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/chunkeey/nu801.git
PKG_SOURCE_VERSION:=39661bfcd0ee9a8e7e9a3e920abe1064c589aaa3

PKG_MAINTAINER:=Christian Lamparter <chunkeey@gmail.com>
PKG_LICENSE:=GPL-3.0-or-later
PKG_LICENSE_FILES:=LICENSE

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

CMAKE_OPTIONS += \
	-DCMAKE_BUILD_TYPE=Debug

define Package/nu801
  SECTION:=utils
  CATEGORY:=Utilities
  SUBMENU:=Userspace GPIO Drivers
  TITLE:=NU801 LED Driver
endef

define Package/nu801/description
This package contains a userspace driver to power the NUMEN Tech. NU801 LED Driver.
endef

define Package/nu801/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/nu801 $(1)/usr/sbin/
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/nu801.init $(1)/etc/init.d/nu801

endef

$(eval $(call BuildPackage,nu801))
