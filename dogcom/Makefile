include $(TOPDIR)/rules.mk

PKG_NAME:=dogcom
PKG_VERSION:=1.0
PKG_RELEASE:=1

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

define Package/dogcom
  SECTION:=net
  CATEGORY:=Network
  TITLE:=Dr.COM Authentication Client
  DEPENDS:=+libpcap +libopenssl
endef

define Package/dogcom/description
  A client for Dr.COM campus network authentication.
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
		CC="$(TARGET_CC)" \
		CFLAGS="$(TARGET_CFLAGS)" \
		LDFLAGS="$(TARGET_LDFLAGS)" \
		DESTDIR="$(PKG_INSTALL_DIR)"
endef

define Package/dogcom/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/dogcom $(1)/usr/bin/
endef

$(eval $(call BuildPackage,dogcom))