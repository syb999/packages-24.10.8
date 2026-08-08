#
# Copyright (C) 2020 Project OpenWrt
# This is free software, licensed under the GNU General Public License v3.
# See /LICENSE.txt for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=filebrowser
PKG_VERSION:=2.32.0
PKG_RELEASE:=1

include $(INCLUDE_DIR)/package.mk

define Package/filebrowser
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=Web File Browser which can be used as a middleware or standalone app.
  URL:=https://github.com/filebrowser/filebrowser
  DEPENDS:=+libpthread
endef

define Package/filebrowser/description
  filebrowser provides a file managing interface within a specified directory
  and it can be used to upload, delete, preview, rename and edit your files.
  It allows the creation of multiple users and each user can have its own directory.
  It can be used as a standalone app or as a middleware.
endef


ifeq ($(ARCH),aarch64)
	filebrowser_ARCH:=arm64
	PKG_HASH:=skip
endif

ifeq ($(ARCH),arm)
	filebrowser_ARCH:=armv7
	PKG_HASH:=skip
endif


ifeq ($(ARCH),x86_64)
	filebrowser_ARCH:=amd64
	PKG_HASH:=skip
endif


PKG_SOURCE_URL:=https://github.com/filebrowser/filebrowser/releases/download/v$(PKG_VERSION)/
PKG_SOURCE:=linux-$(filebrowser_ARCH)-filebrowser.tar.gz

define Build/Prepare
	$(TAR) -C $(PKG_BUILD_DIR) -xzf $(DL_DIR)/$(PKG_SOURCE) --strip-components=0
endef

define Build/Compile
endef

define Package/filebrowser/install
	$(INSTALL_DIR) $(1)/etc/config/ $(1)/etc/init.d/ $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/filebrowser $(1)/usr/bin
	$(INSTALL_CONF) ./files/filebrowser.config $(1)/etc/config/filebrowser
	$(INSTALL_BIN) ./files/filebrowser.init $(1)/etc/init.d/filebrowser
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
