#
# Copyright (C) 2020 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=armbian-firmware
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_DATE:=2024-08-15
PKG_SOURCE_URL:=https://proxy.vvvv.ee/https://github.com/armbian/firmware.git
PKG_SOURCE_VERSION:=511deee7289cb9a5dee6ba142d18a09933d5ba00
PKG_MIRROR_HASH:=918f05ad98cb4a6fdd713b874d794d1aefc2a644025bca418f877c5f9c0f60c5

include $(INCLUDE_DIR)/package.mk

define Package/brcmfmac-firmware-default
  SECTION:=firmware
  CATEGORY:=Firmware
  TITLE:=Broadcom FullMac SDIO firmware
  URL:=https://proxy.vvvv.ee/https://github.com/armbian/firmware
endef

define Package/brcmfmac-firmware-43752-sdio
  $(Package/brcmfmac-firmware-default)
  TITLE:=Broadcom BRCM43752 FullMac SDIO firmware
endef

define Package/brcmfmac-firmware-43430b0-sdio
  $(Package/brcmfmac-firmware-default)
  TITLE:=Broadcom BCM43430B0 FullMac SDIO firmware
endef

define Package/brcmfmac-nvram-43430b0-sdio
  $(Package/brcmfmac-firmware-default)
  TITLE:=Broadcom BCM43430B0 SDIO NVRAM firmware
endef

#添加AW859a(uwe5622)驱动
define Package/uwe5622-firmware
        $(Package/brcmfmac-firmware-default)
        URL:=$(PKG_SOURCE_URL)
        DEPENDS:=
        TITLE:=Unisoc UWE5622 firmware(orangepi zero 2)
endef

define Build/Compile
        true
endef

define Package/brcmfmac-firmware-43752-sdio/install
        $(INSTALL_DIR) $(1)/lib/firmware/brcm
        $(INSTALL_DATA) \
                $(PKG_BUILD_DIR)/brcm/BCM4362A2.hcd \
                $(1)/lib/firmware/brcm/BCM4362A2.hcd
        $(INSTALL_DATA) \
                $(PKG_BUILD_DIR)/brcm/brcmfmac43752-sdio.bin \
                $(1)/lib/firmware/brcm/brcmfmac43752-sdio.bin
        $(INSTALL_DATA) \
                $(PKG_BUILD_DIR)/brcm/brcmfmac43752-sdio.clm_blob \
                $(1)/lib/firmware/brcm/brcmfmac43752-sdio.clm_blob
        $(INSTALL_DATA) \
                $(PKG_BUILD_DIR)/brcm/brcmfmac43752-sdio.txt \
                $(1)/lib/firmware/brcm/brcmfmac43752-sdio.txt
        $(LN) \
                brcmfmac43752-sdio.txt \
                $(1)/lib/firmware/brcm/brcmfmac43752-sdio.armsom,sige1.txt
        $(LN) \
                brcmfmac43752-sdio.txt \
                $(1)/lib/firmware/brcm/brcmfmac43752-sdio.armsom,sige3.txt
endef

$(eval $(call BuildPackage,brcmfmac-firmware-43752-sdio))

define Package/brcmfmac-firmware-43430b0-sdio/install
        $(INSTALL_DIR) $(1)/lib/firmware/brcm
        $(INSTALL_DATA) \
                $(PKG_BUILD_DIR)/brcm/BCM43430B0.hcd \
                $(1)/lib/firmware/brcm/
        $(INSTALL_DATA) \
                $(PKG_BUILD_DIR)/brcm/brcmfmac43430b0-sdio.bin \
                $(1)/lib/firmware/brcm/
        $(INSTALL_DATA) \
                $(PKG_BUILD_DIR)/brcm/brcmfmac43430-sdio.clm_blob \
                $(1)/lib/firmware/brcm/
endef
$(eval $(call BuildPackage,brcmfmac-firmware-43430b0-sdio))

define Package/brcmfmac-nvram-43430b0-sdio/install
        $(INSTALL_DIR) $(1)/lib/firmware/brcm
        $(INSTALL_DATA) \
                $(PKG_BUILD_DIR)/brcm/brcmfmac43430b0-sdio.txt \
                $(1)/lib/firmware/brcm/
        $(LN) \
                brcmfmac43430b0-sdio.txt \
                $(1)/lib/firmware/brcm/brcmfmac43430b0-sdio.rumu3f,fine-3399.txt
endef
$(eval $(call BuildPackage,brcmfmac-nvram-43430b0-sdio))

define Package/uwe5622-firmware/install
        $(INSTALL_DIR) $(1)/lib/firmware
        $(INSTALL_DATA) \
                $(PKG_BUILD_DIR)/uwe5622/wcnmodem.bin \
                $(PKG_BUILD_DIR)/uwe5622/wcnmodem-38222.bin \
                $(PKG_BUILD_DIR)/uwe5622/wifi_2355b001_1ant.ini \
                $(1)/lib/firmware/
endef

$(eval $(call BuildPackage,uwe5622-firmware))
