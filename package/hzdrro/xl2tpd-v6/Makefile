#
# Copyright (C) 2006-2015 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=xl2tpd
PKG_VERSION:=1.3.18-ipv6
PKG_RELEASE:=1
PKG_MAINTAINER:=Yousong Zhou <yszhou4tech@gmail.com>
PKG_LICENSE:=GPL-2.0
PKG_LICENSE_FILES:=LICENSE

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/hzdrro/xl2tpd.git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=v$(PKG_VERSION)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_MIRROR_HASH:=caf8d8e2acec6182c0c2b211b7f9394832c0785dd3ff465c211865ae892107be

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/xl2tpd-v6
  SECTION:=net
  CATEGORY:=Network
  TITLE:=An L2TP (Layer 2 Tunneling Protocol) daemon
  URL:=http://www.xelerance.com/software/xl2tpd/
  SUBMENU:=VPN
  DEPENDS:=+ppp-mod-pppol2tp +resolveip
endef

define Package/xl2tpd-v6/description
l2tpd is the open source implementation of the L2TP tunneling protocol (RFC2661).
It does implement both LAC and LNS role in a L2TP networking architecture. The
main goal of this protocol is to tunnel PPP frame trough an IP network.
endef

ifneq (0,0)
  # debugging options from Makefile of xl2tpd package
  EXTRA_CFLAGS += \
	-DDEBUG_ZLB \
	-DDEBUG_HELLO \
	-DDEBUG_CLOSE \
	-DDEBUG_FLOW \
	-DDEBUG_FILE \
	-DDEBUG_AAA \
	-DDEBUG_PAYLOAD \
	-DDEBUG_CONTROL \
	-DDEBUG_PPPD \
	-DDEBUG_HIDDEN \
	-DDEBUG_ENTROPY \
	-DDEBUG_CONTROL_XMIT \
	-DDEBUG_MAGIC \
	-DDEBUG_FLOW_MORE \
	-DDEBUG_AUTH
endif

define Package/xl2tpd-v6/conffiles
/etc/xl2tpd/xl2tpd.conf
/etc/xl2tpd/xl2tp-secrets
/etc/ppp/options.xl2tpd
endef

define Package/xl2tpd-v6/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/local/sbin/xl2tpd $(1)/usr/sbin/
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/local/sbin/xl2tpd-control $(1)/usr/sbin/

	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/xl2tpd.init $(1)/etc/init.d/xl2tpd

	$(INSTALL_DIR) $(1)/etc/xl2tpd
	$(INSTALL_DATA) ./files/xl2tpd.conf $(1)/etc/xl2tpd/
	$(INSTALL_CONF) ./files/xl2tp-secrets $(1)/etc/xl2tpd/

	$(INSTALL_DIR) $(1)/etc/ppp
	$(INSTALL_DATA) ./files/options.xl2tpd $(1)/etc/ppp/

	$(INSTALL_DIR) $(1)/lib/netifd/proto
	$(INSTALL_BIN) ./files/l2tp.sh $(1)/lib/netifd/proto
endef

$(eval $(call BuildPackage,xl2tpd-v6))
