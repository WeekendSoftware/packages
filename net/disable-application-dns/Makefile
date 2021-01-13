#
# Copyright (c) 2018 Gregory L. Dietsche <Gregory.Dietsche@cuw.edu>
# This is free software, licensed under the MIT License
#

include $(TOPDIR)/rules.mk

PKG_NAME:=disable-application-dns
PKG_VERSION:=1.0.0
PKG_RELEASE:=1
PKG_LICENSE:=MIT
PKG_MAINTAINER:=Gregory L. Dietsche <Gregory.Dietsche@cuw.edu>

include $(INCLUDE_DIR)/package.mk

define Package/disable-application-dns
	SECTION:=net
	CATEGORY:=Network
	TITLE:=Disable Application DNS
	PKGARCH:=all
endef

define Package/disable-application-dns/description
This package tells Firefox and any other application that checks
use-application-dns.net that it should disable application DNS (e.g. DoH)
and send DNS queries to your router instead of bypassing your router.

For more information, please visit:
https://support.mozilla.org/en-US/kb/canary-domain-use-application-dnsnet
endef

define Build/Compile
endef

define Package/disable-application-dns/install
	$(INSTALL_DIR) $(1)/etc/uci-defaults
	$(CP) ./files/disable-application-dns.defaults $(1)/etc/uci-defaults/disable-application-dns
endef

define Package/disable-application-dns/prerm
#!/bin/sh
if [ -z "$${IPGK_INSTROOT}" ]; then
	uci del_list dhcp.@dnsmasq[0].address=/use-application-dns.net/
	uci commit dhcp
	/etc/init.d/dnsmasq reload
fi
exit 0
endef

$(eval $(call BuildPackage,disable-application-dns))
