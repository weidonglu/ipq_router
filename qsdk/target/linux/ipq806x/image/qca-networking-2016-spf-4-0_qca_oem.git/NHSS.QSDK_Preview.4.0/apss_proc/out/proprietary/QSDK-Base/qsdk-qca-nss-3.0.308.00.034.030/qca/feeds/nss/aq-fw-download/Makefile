include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=aq-fw-download
PKG_BRANCH:=master
PKG_VERSION:=1.0
PKG_RELEASE:=1

PKG_BUILD_DIR:=$(BUILD_DIR)/aq-fw-download

-include $(INCLUDE_DIR)/package-version-override.mk
include $(INCLUDE_DIR)/package.mk

define AquantiaUtil

  define Package/aq-fw-download
    SECTION:=QCA
    CATEGORY:=QCA Proprietary software
    DEPENDS:=@TARGET_ipq806x
    TITLE:=Aquantia FW downloader utitlity
  endef

  define Package/aq-fw-download/description
  Aquantia FW downloader utitlity
  endef

  define Package/aq-fw-download/config
  $(call Package/aq-fw-download/override_source_path,aq-fw-download)
  endef

TARGET_CPPFLAGS := \
	-D_GNU_SOURCE \
	-I$(LINUX_SRC_DIR)/include \
	-I$(LINUX_SRC_DIR)/arch/$(LINUX_KARCH)/include \
	-I$(PKG_BUILD_DIR) \
	$(TARGET_CPPFLAGS)

 define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	$(CP) ./src/* $(PKG_BUILD_DIR)/
 endef

 define Build/Compile
	CFLAGS="$(TARGET_CPPFLAGS) $(TARGET_CFLAGS)" \
	LDFLAGS="$(TARGET_LDFLAGS)" \
	$(MAKE) -C $(PKG_BUILD_DIR) \
		$(TARGET_CONFIGURE_OPTS)
 endef

 define Package/aq-fw-download/install
	$(INSTALL_DIR) $$(1)/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/aq-fw-download $$(1)/sbin/aq-fw-download
 endef

  $$(eval $$(call BuildPackage,aq-fw-download))
endef

#Build/Compile=true

$(eval $(call AquantiaUtil))
