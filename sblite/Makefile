include $(TOPDIR)/rules.mk

PKG_NAME:=sblite
PKG_VERSION:=0.1.4
PKG_RELEASE:=1

ifeq ($(ARCH),x86_64)
  RELEASE_ARCH:=amd64
endif
ifeq ($(ARCH),aarch64)
  RELEASE_ARCH:=arm64
endif

PKG_SOURCE:=$(PKG_NAME)-$(RELEASE_ARCH)-linux.tar.gz
PKG_SOURCE_URL:=https://github.com/RMTT/sb-lite/releases/download/v$(PKG_VERSION)/
PKG_HASH:=skip

PKG_LICENSE:=MIT
PKG_MAINTAINER:=RMTT

include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)
  SECTION:=net
  CATEGORY:=Network
  TITLE:=sb-lite Proxy Tool
  URL:=https://github.com/RMTT/sb-lite
endef

define Package/$(PKG_NAME)/description
  sb-lite proxy tool, repackaged from GitHub pre-compiled releases into an OpenWrt apk.
endef
define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	tar -xzvf $(DL_DIR)/$(PKG_SOURCE) -C $(PKG_BUILD_DIR)
endef

define Build/Configure
endef

define Build/Compile
endef

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/$(PKG_NAME)-$(RELEASE_ARCH)-linux $(1)/usr/bin/

	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/sblite.init $(1)/etc/init.d/sblite
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
