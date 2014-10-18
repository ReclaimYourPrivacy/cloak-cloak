#
# Copyright (c) 2014 Bright Things Ltd. All right reserved.
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=cloak
PKG_VERSION:=0.0.1
PKG_RELEASE:=1

include $(INCLUDE_DIR)/package.mk

define Package/cloak
  SECTION:=utils
  CATEGORY:=Cloak
  TITLE:=Default Cloak Configurations
  DEPENDS:=+base-files +luci +luci-proto-3g +luci-proto-ipv6 +luci-proto-ppp +6in4 +6rd +6to4 +curl +ip +kmod-usb-serial +kmod-usb-serial-option +iwinfo +avahi-daemon +avahi-utils
endef

define Package/cloak/conffiles
/etc/shadow
endef

define Build/Compile
	# NOOP
endef

define Package/cloak/install
	$(INSTALL_DIR) $(1)/etc/uci-defaults
	$(INSTALL_CONF) ./files/etc/shadow $(1)/etc
	$(INSTALL_CONF) ./files/etc/banner $(1)/etc
	$(INSTALL_BIN) ./files/etc/uci-defaults/70-firewall $(1)/etc/uci-defaults
	$(INSTALL_BIN) ./files/etc/uci-defaults/70-hostname $(1)/etc/uci-defaults
	$(INSTALL_BIN) ./files/etc/uci-defaults/70-uhttpd $(1)/etc/uci-defaults
endef

$(eval $(call BuildPackage,cloak))

