include $(TOPDIR)/rules.mk

PKG_NAME:=udp2raw
PKG_VERSION:=20230206.0
PKG_RELEASE:=1

PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE
PKG_MAINTAINER:=Yu Wang

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk

define Package/udp2raw
	SECTION:=net
	CATEGORY:=Network
	TITLE:=Tunnel which turns UDP Traffic into Encrypted FakeTCP/UDP/ICMP Traffic
	URL:=https://github.com/wangyu-/udp2raw-tunnel
endef

define Package/udp2raw/description
	udp2raw-tunnel is a tunnel which turns UDP Traffic into Encrypted FakeTCP/UDP/ICMP Traffic by using Raw Socket.
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	$(CP) $(CURDIR)/src/* $(PKG_BUILD_DIR)/
endef

MAKE_FLAGS += cross2

define Build/Configure
	$(SED) 's/cc_cross[[:space:]]*=.*/cc_cross=$(TARGET_CXX)/' \
		-e 's/\\".*shell git rev-parse HEAD.*\\"/\\"$(PKG_VERSION)\\"/' \
		$(PKG_BUILD_DIR)/makefile
endef

define Package/udp2raw/conffiles
/etc/udp2raw/default.conf
endef

define Package/udp2raw/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/udp2raw_cross $(1)/usr/bin/udp2raw
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/udp2raw.init $(1)/etc/init.d/udp2raw
	$(INSTALL_DIR) $(1)/etc/udp2raw
	$(INSTALL_CONF) ./files/udp2raw.conf $(1)/etc/udp2raw/default.conf
endef

$(eval $(call BuildPackage,udp2raw))
