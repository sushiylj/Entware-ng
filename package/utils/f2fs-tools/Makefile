#
# Copyright (C) 2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=f2fs-tools
PKG_VERSION:=1.8.0
PKG_RELEASE:=2

PKG_LICENSE:=GPLv2

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://git.kernel.org/pub/scm/linux/kernel/git/jaegeuk/f2fs-tools.git/snapshot/
PKG_HASH:=d4dbecf55560c548bf0758c9f641d1beec1e960b38cbbc19951195d5144d39ae

PKG_FIXUP:=autoreconf
PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1

PKG_MAINTAINER:=Felix Fietkau <nbd@nbd.name>

include $(INCLUDE_DIR)/package.mk

define Package/f2fs-tools/Default
  SECTION:=utils
  CATEGORY:=Utilities
  SUBMENU:=Filesystem
  DEPENDS:=+libf2fs
  URL:=http://git.kernel.org/cgit/linux/kernel/git/jaegeuk/f2fs-tools.git
endef

define Package/mkf2fs
  $(Package/f2fs-tools/Default)
  TITLE:=Utility for creating a Flash-Friendly File System (F2FS)
endef

define Package/f2fsck
  $(Package/f2fs-tools/Default)
  TITLE:=Utility for checking/repairing a Flash-Friendly File System (F2FS)
endef

define Package/f2fs-tools
  $(Package/f2fs-tools/Default)
  TITLE:=Tools for Flash-Friendly File System (F2FS)
  DEPENDS += +mkf2fs +f2fsck
endef

define Package/libf2fs
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=Library for Flash-Friendly File System (F2FS) tools
  DEPENDS:=+libuuid
endef

CONFIGURE_ARGS += \
	--without-selinux

define Package/libf2fs/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) \
		$(PKG_INSTALL_DIR)/opt/lib/libf2fs.so* $(1)/opt/lib/
endef

define Package/mkf2fs/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/sbin/mkfs.f2fs $(1)/opt/sbin
endef

define Package/f2fsck/install
	$(INSTALL_DIR) $(1)/opt/sbin

	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/sbin/fsck.f2fs $(1)/opt/sbin
	ln -s fsck.f2fs $(1)/opt/sbin/defrag.f2fs
	ln -s fsck.f2fs $(1)/opt/sbin/dump.f2fs
	ln -s fsck.f2fs $(1)/opt/sbin/sload.f2fs
	ln -s fsck.f2fs $(1)/opt/sbin/resize.f2fs
endef

define Package/f2fs-tools/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/sbin/f2fstat $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/sbin/fibmap.f2fs $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/sbin/parse.f2fs $(1)/opt/sbin
endef

$(eval $(call BuildPackage,libf2fs))
$(eval $(call BuildPackage,mkf2fs))
$(eval $(call BuildPackage,f2fsck))
$(eval $(call BuildPackage,f2fs-tools))
