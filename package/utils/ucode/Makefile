#
# Copyright (C) 2020-2021 Jo-Philipp Wich <jo@mein.io>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=ucode
PKG_RELEASE:=2

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL=https://github.com/jow-/ucode.git
PKG_SOURCE_DATE:=2021-10-25
PKG_SOURCE_VERSION:=a7976c2802a9da737f62bec496c7115211c442a7
PKG_MIRROR_HASH:=6bc3ddeef41d68fd96894957356472e576c625fcf7277cbb36aa464b8d3c274d
PKG_MAINTAINER:=Jo-Philipp Wich <jo@mein.io>
PKG_LICENSE:=ISC

PKG_ABI_VERSION:=20210730

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

CMAKE_OPTIONS += -DSOVERSION=$(PKG_ABI_VERSION)

define Package/ucode/default
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=ucode - Tiny scripting and templating language
endef

define Package/ucode
  $(Package/ucode/default)
  DEPENDS:=+libucode
endef

define Package/ucode/description
 ucode is a tiny script interpreter featuring an ECMAScript oriented
 script language and Jinja-inspired templating.
endef


define Package/libucode
  $(Package/ucode/default)
  TITLE+= - runtime library
  ABI_VERSION:=$(PKG_ABI_VERSION)
  DEPENDS:=+libjson-c
endef

define Package/libucode/description
 The libucode package provides the shared runtime library for the ucode interpreter.
endef


define Package/ucode-mod-fs
  $(Package/ucode/default)
  TITLE+= (filesystem module)
  DEPENDS:=ucode
endef

define Package/ucode-mod-fs/description
 The filesystem plugin module allows interaction with the local file system.
endef


define Package/ucode-mod-math
  $(Package/ucode/default)
  TITLE+= (math module)
  DEPENDS:=ucode
endef

define Package/ucode-mod-math/description
 The math plugin provides access to various <math.h> procedures.
endef


define Package/ucode-mod-nl80211
  $(Package/ucode/default)
  TITLE+= (nl80211 module)
  DEPENDS:=ucode +libnl-tiny
endef

define Package/ucode-mod-nl80211/description
 The nl80211 plugin provides access to the Linux wireless 802.11 netlink API.
endef


define Package/ucode-mod-resolv
  $(Package/ucode/default)
  TITLE+= (resolv module)
  DEPENDS:=ucode
endef

define Package/ucode-mod-resolv/description
 The resolv plugin implements simple DNS resolving.
endef


define Package/ucode-mod-rtnl
  $(Package/ucode/default)
  TITLE+= (rtnl module)
  DEPENDS:=ucode +libnl-tiny
endef

define Package/ucode-mod-rtnl/description
 The rtnl plugin provides access to the Linux routing netlink API.
endef


define Package/ucode-mod-ubus
  $(Package/ucode/default)
  TITLE+= (ubus module)
  DEPENDS:=ucode +libubus +libblobmsg-json
endef

define Package/ucode-mod-ubus/description
 The ubus module allows ucode template scripts to enumerate and invoke ubus
 procedures.
endef


define Package/ucode-mod-uci
  $(Package/ucode/default)
  TITLE+= (uci module)
  DEPENDS:=ucode +libuci
endef

define Package/ucode-mod-uci/description
 The uci module allows templates to read and modify uci configuration.
endef


define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/lib $(1)/usr/include/ucode
	$(CP) $(PKG_INSTALL_DIR)/usr/include/ucode/*.h $(1)/usr/include/ucode/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libucode.so* $(1)/usr/lib/
endef


define Package/ucode/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/ucode $(1)/usr/bin/ucode
endef

define Package/libucode/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libucode.so.* $(1)/usr/lib/
endef

define Package/ucode-mod-fs/install
	$(INSTALL_DIR) $(1)/usr/lib/ucode
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/lib/ucode/fs.so $(1)/usr/lib/ucode/
endef

define Package/ucode-mod-math/install
	$(INSTALL_DIR) $(1)/usr/lib/ucode
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/lib/ucode/math.so $(1)/usr/lib/ucode/
endef

define Package/ucode-mod-nl80211/install
	$(INSTALL_DIR) $(1)/usr/lib/ucode
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/lib/ucode/nl80211.so $(1)/usr/lib/ucode/
endef

define Package/ucode-mod-resolv/install
	$(INSTALL_DIR) $(1)/usr/lib/ucode
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/lib/ucode/resolv.so $(1)/usr/lib/ucode/
endef

define Package/ucode-mod-rtnl/install
	$(INSTALL_DIR) $(1)/usr/lib/ucode
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/lib/ucode/rtnl.so $(1)/usr/lib/ucode/
endef

define Package/ucode-mod-ubus/install
	$(INSTALL_DIR) $(1)/usr/lib/ucode
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/lib/ucode/ubus.so $(1)/usr/lib/ucode/
endef

define Package/ucode-mod-uci/install
	$(INSTALL_DIR) $(1)/usr/lib/ucode
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/lib/ucode/uci.so $(1)/usr/lib/ucode/
endef


$(eval $(call BuildPackage,ucode))
$(eval $(call BuildPackage,libucode))
$(eval $(call BuildPackage,ucode-mod-fs))
$(eval $(call BuildPackage,ucode-mod-math))
$(eval $(call BuildPackage,ucode-mod-nl80211))
$(eval $(call BuildPackage,ucode-mod-resolv))
$(eval $(call BuildPackage,ucode-mod-rtnl))
$(eval $(call BuildPackage,ucode-mod-ubus))
$(eval $(call BuildPackage,ucode-mod-uci))
