#
# Copyright (C) 2017 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=tang
PKG_VERSION:=6
PKG_RELEASE:=1

#PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
#PKG_SOURCE_URL:=https://github.com/latchset/$(PKG_NAME)/releases/download/v$(PKG_VERSION)/
#PKG_HASH:=1df78b48a52d2ca05656555cfe52bd4427c884f5a54a2c5e37a7b39da9e155e3

PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1

PKG_FIXUP:=autoreconf

include $(INCLUDE_DIR)/package.mk

define Package/tang
  SECTION:=utils
  TITLE:=tang v$(PKG_VERSION) - daemon for binding data to the presence of a third party
  DEPENDS:=+libhttp-parser +xinetd +jose +bash
  URL:=https://github.com/latchset/tang
endef

CFLAGS += -fhonour-copts
TARGET_CFLAGS += $(FPIC) -std=gnu99 -D_GNU_SOURCE
TARGET_LDFLAGS += -Wl,-rpath-link=$(1)/usr/lib

define Build/Prepare
	$(CP) ./src/* $(PKG_BUILD_DIR)/
endef

define Package/tang/description
	Tang is a small daemon for binding data to the presence of a third party.
endef

define Build/Configure
	$(call Build/Configure/Default)
endef

define Package/tang/install
	$(INSTALL_DIR)	$(1)/usr/libexec
	$(INSTALL_DIR)	$(1)/etc/$(PKG_NAME)i/db
	$(INSTALL_DIR)	$(1)/etc/$(PKG_NAME)/cache
	$(INSTALL_DIR)	$(1)/etc/xinetd.d/
	$(INSTALL_BIN)	$(PKG_INSTALL_DIR)/usr/lib/$(PKG_NAME)d		$(1)/usr/libexec/
	$(INSTALL_BIN)	$(PKG_INSTALL_DIR)/usr/lib/$(PKG_NAME)d-update	$(1)/usr/libexec/
	$(INSTALL_BIN)	$(PKG_INSTALL_DIR)/usr/lib/$(PKG_NAME)d-keygen	$(1)/usr/libexec/
	$(INSTALL_BIN)	$(PKG_BUILD_DIR)/tangdw				$(1)/usr/libexec/
	$(CP)		$(PKG_BUILD_DIR)/tangdx				$(1)/etc/xinetd.d/
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
