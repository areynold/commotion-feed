include $(TOPDIR)/rules.mk

MODULE_NAME:=commotion
MODULE_TITLE:=Commotion

PKG_NAME:=luci-$(MODULE_NAME)
PKG_VERSION:=1.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=git://github.com/opentechinstitute/luci-commotion.git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=$(PKG_VERSION)

PKG_SOURCE:=$(PKG_NAME)-$(PKG_SOURCE_VERSION).tar.gz
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

define Package/luci-$(MODULE_NAME)
  SECTION:=luci
  CATEGORY:=LuCI
  SUBMENU:=2. Modules
  DEPENDS:=+commotionbase
  TITLE:=LuCI Module - $(MODULE_TITLE)
  URL:=https://commotionwireless.net/
endef

define Build/Configure
endef

define Build/Compile
endef

define Package/luci-commotion/description
  Commotion project webGUI add-on
endef

define Package/luci-$(MODULE_NAME)/install
	$(INSTALL_DIR) $(1)/etc/uci-defaults
	$(CP) -a ./files/etc/uci-defaults/* $(1)/etc/uci-defaults/ 2>/dev/null || true
	$(INSTALL_DIR) $(1)/usr/share/commotion/files
	$(CP) -a ./files/usr/share/commotion/files/* $(1)/usr/share/commotion/files/ 2>/dev/null || true
	$(INSTALL_DIR) $(1)/usr/lib/lua/luci/controller/$(MODULE_NAME)
	$(CP) -a ./luasrc/controller/$(MODULE_NAME)/* $(1)/usr/lib/lua/luci/controller/$(MODULE_NAME)/ 2>/dev/null || true
	$(INSTALL_DIR) $(1)/usr/lib/lua/luci/model/cbi/$(MODULE_NAME)
	$(CP) -a ./luasrc/model/cbi/$(MODULE_NAME)/* $(1)/usr/lib/lua/luci/model/cbi/$(MODULE_NAME)/ 2>/dev/null || true
	$(INSTALL_DIR) $(1)/usr/lib/lua/luci/model/cbi/admin_network
	$(CP) -a ./luasrc/model/cbi/admin_network/* $(1)/usr/lib/lua/luci/model/cbi/admin_network/ 2>/dev/null || true
	$(INSTALL_DIR) $(1)/usr/lib/lua/luci/model/network
	$(CP) -a ./luasrc/model/network/* $(1)/usr/lib/lua/luci/model/network/ 2>/dev/null || true
	$(INSTALL_DIR) $(1)/usr/lib/lua/luci/view/$(MODULE_NAME)
	$(CP) -a ./luasrc/view/$(MODULE_NAME)/* $(1)/usr/lib/lua/luci/view/$(MODULE_NAME)/ 2>/dev/null || true
	$(INSTALL_DIR) $(1)/usr/lib/lua/luci/view/cbi
	$(CP) -a ./luasrc/view/cbi/* $(1)/usr/lib/lua/luci/view/cbi/ 2>/dev/null || true
	$(INSTALL_DIR) $(1)/www/luci-static/resources/
	$(CP) -a ./htdocs/luci-static/* $(1)/www/luci-static/ 2>/dev/null || true
endef

define Package/luci-$(MODULE_NAME)/postinst
#!/bin/sh
[ -n "$${IPKG_INSTROOT}" ] || {
	( . /etc/uci-defaults/luci-$(MODULE_NAME) ) && rm -f /etc/uci-defaults/luci-$(MODULE_NAME)
}
endef

$(eval $(call BuildPackage,luci-$(MODULE_NAME)))
