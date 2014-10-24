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
  DEPENDS:=+base-files +luci +luci-proto-3g +luci-proto-ipv6 +luci-proto-ppp +6in4 +6rd +6to4 +curl +ip +kmod-usb-serial +kmod-usb-serial-option +iwinfo +avahi-daemon +avahi-utils +block-mount +chat +comgt +kmod-fs-vfat +kmod-nls-cp437 +kmod-nls-cp850 +kmod-nls-iso8859-1 +kmod-nls-utf8 +pptp +kmod-usb-storage +kmod-usb-storage-extras +tor-cloak
endef

define Package/cloak/conffiles
/etc/config/dhcp
/etc/config/dropbear
/etc/config/firewall
/etc/config/luci
/etc/config/network
/etc/config/system
/etc/config/tor
/etc/config/uhttpd
/etc/config/wireless
endef

define Build/Compile
	# NOOP
endef

define Package/cloak/install
	$(INSTALL_DIR) $(1)/etc
	$(INSTALL_DIR) $(1)/etc/uci-defaults
	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_CONF) ./files/etc/config/dhcp $(1)/etc/config/
	$(INSTALL_CONF) ./files/etc/config/dropbear $(1)/etc/config/
	$(INSTALL_CONF) ./files/etc/config/firewall $(1)/etc/config/
	$(INSTALL_CONF) ./files/etc/config/luci $(1)/etc/config/
	$(INSTALL_CONF) ./files/etc/config/network $(1)/etc/config/
	$(INSTALL_CONF) ./files/etc/config/system $(1)/etc/config/
	$(INSTALL_CONF) ./files/etc/config/tor $(1)/etc/config/
	$(INSTALL_CONF) ./files/etc/config/uhttpd $(1)/etc/config/
	$(INSTALL_CONF) ./files/etc/config/wireless $(1)/etc/config/
	$(INSTALL_BIN) ./files/etc/banner $(1)/etc/
	$(INSTALL_BIN) ./files/etc/init.d/cloak $(1)/etc/init.d/
	$(INSTALL_BIN) ./files/etc/uci-defaults/70-hostname $(1)/etc/uci-defaults
endef

$(eval $(call BuildPackage,cloak))

