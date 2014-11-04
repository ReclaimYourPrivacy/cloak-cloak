#
# Copyright (C) 2014 Bright-Things.com
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=tor-cloak
PKG_VERSION:=0.2.5.10
PKG_RELEASE:=1

PKG_SOURCE:=tor-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://www.torproject.org/dist \
	https://archive.torproject.org/tor-package-archive
PKG_MD5SUM:=4bde375229a7a7f77c0596ae05556527

PKG_BUILD_DEPENDS:=libminiupnpc libnatpmp
PKG_BUILD_DIR:=$(BUILD_DIR)/tor-$(PKG_VERSION)
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/tor-cloak/Default
  SECTION:=net
  CATEGORY:=Network
  URL:=https://www.torproject.org/
endef

define Package/tor-cloak/Default/description
 Tor is a toolset for a wide range of organizations and people that want to
 improve their safety and security on the Internet. Using Tor can help you
 anonymize web browsing and publishing, instant messaging, IRC, SSH, and
 more. Tor also provides a platform on which software developers can build
 new applications with built-in anonymity, safety, and privacy features.

 This version contains changes made for Cloak
endef

define Package/tor-cloak
$(call Package/tor-cloak/Default)
  TITLE:=An anonymous Internet communication system
  DEPENDS:=+libevent2 +libopenssl +libpthread +librt +SSP_SUPPORT:libssp
endef

define Package/tor-cloak/description
$(call Package/tor-cloak/Default/description)
 This package contains the tor daemon.
endef

define Package/tor-cloak-fw-helper
$(call Package/tor-cloak/Default)
  TITLE:=Firewall helper for tor
  DEPENDS:=+tor-cloak +libminiupnpc +libnatpmp
endef

define Package/tor-cloak-fw-helper/description
$(call Package/tor-cloak/Default/description)
 This package contains a helper for automatically configuring port forwarding.
endef

define Package/tor-cloak-geoip
$(call Package/tor-cloak/Default)
  TITLE:=GeoIP db for tor
  DEPENDS:=+tor-cloak
endef

define Package/tor-cloak-geoip/description
$(call Package/tor-cloak/Default/description)
 This package contains a GeoIP database mapping IP addresses to countries.
endef

define Package/tor-cloak/conffiles
/etc/config/tor
endef

CONFIGURE_ARGS += \
	--with-libevent-dir="$(STAGING_DIR)/usr" \
	--with-ssl-dir="$(STAGING_DIR)/usr" \
	--with-libminiupnpc-dir="$(STAGING_DIR)/usr" \
	--with-libnatpmp-dir="$(STAGING_DIR)/usr" \
	--disable-asciidoc \
	--disable-threads

ifneq ($(CONFIG_SSP_SUPPORT),y)
	CONFIGURE_ARGS += \
		--disable-gcc-hardening
	MAKE_FLAGS += \
		CFLAGS="$(TARGET_CFLAGS)"
else
	MAKE_FLAGS += \
		CFLAGS="$(TARGET_CFLAGS) -fPIC"

endif

CONFIGURE_VARS += \
	CROSS_COMPILE="yes"

define Package/tor-cloak/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/tor $(1)/usr/sbin/
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_BIN) ./files/tor.init $(1)/etc/init.d/tor
	$(INSTALL_CONF) ./files/tor.config $(1)/etc/config/tor
endef

define Package/tor-cloak-fw-helper/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/tor-fw-helper $(1)/usr/bin/
endef

define Package/tor-cloak-geoip/install
	$(INSTALL_DIR) $(1)/usr/share/tor
	$(CP) $(PKG_INSTALL_DIR)/usr/share/tor/geoip $(1)/usr/share/tor/
endef

$(eval $(call BuildPackage,tor-cloak))
$(eval $(call BuildPackage,tor-cloak-fw-helper))
$(eval $(call BuildPackage,tor-cloak-geoip))
