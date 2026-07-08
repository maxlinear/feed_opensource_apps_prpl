#
# Copyright (C) 2023 MaxLinear, Inc.
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=liboptee-client

PKG_SOURCE_PROTO:=git
PKG_VERSION:=4.0.0
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL=https://github.com/OP-TEE/optee_client.git
PKG_SOURCE_VERSION:=4.0.0
PKG_MIRROR_HASH:=2ed6d178a7dcc53771a7e5d7499dfbf4b781379ed54d2860d93e2c4dffc7267b

PKG_LICENSE:=BSD2-clause
PKG_LICENSE_FILES:=LICENSE

export WITH_TEEACL:=0

include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=OP TEE client library
  URL:=https://github.com/OP-TEE/optee_client.git
  DEPENDS:=+libc
endef

define Package/$(PKG_NAME)/description
  TEE client library in Linux provides the TEE Client API as defined by the GlobalPlatform TEE standard.
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) CC="$(TARGET_CC)" \
		CFLAGS="$(TARGET_CFLAGS)" LDFLAGS="$(TARGET_LDFLAGS)" \
		AR="$(TARGET_AR)"
endef

define Build/InstallDev
	$(INSTALL_DIR) $(STAGING_DIR)/usr/lib
	$(INSTALL_DIR) $(STAGING_DIR)/usr/include/
	$(CP) $(PKG_BUILD_DIR)/out/export/usr/include/*.h $(STAGING_DIR)/usr/include/
	$(CP) $(PKG_BUILD_DIR)/out/export/usr/lib/* $(STAGING_DIR)/usr/lib/
endef

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/$(VENDOR_PATH)/usr/lib
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/out/export/usr/lib/libteec.so* $(1)/$(VENDOR_PATH)/usr/lib/
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
