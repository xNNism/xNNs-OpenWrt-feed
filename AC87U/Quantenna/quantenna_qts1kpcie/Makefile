include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=qts1kpcie
PKG_VERSION:=37.3.1.25-OPENWRT
PKG_RELEASE:=1
PKG_BUILD_DIR:=$(KERNEL_BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

PKG_SOURCE:=quantenna_sources.tar.gz
PKG_SOURCE_VERSION:=1.0
PKG_SOURCE_URL:=https://cdn.rawgit.com/xNNism/xNNs-OpenWrt-feed/Asus-RT-AC87U/AC87U/Quantenna/src/
PKG_MD5SUM:=152aabe66b4ca4e6ec658b37847b36d0

include $(INCLUDE_DIR)/package.mk


define KernelPackage/qts1kpcie
  SECTION:=xNN's Feed
  CATEGORY:=xNN's Feed
  SUBMENU:=ASUS RT-AC87U
  MENU:=1
  TITLE:=Quantenna QTS1000 Driver
  DEPENDS:=@PCI_SUPPORT +@DRIVER_WEXT_SUPPORT +qts1kpcierpc
  FILES:= $(PKG_BUILD_DIR)/../quantenna/pcie2/host/arm/qdpc-host.ko
  AUTOLOAD:=$(call AutoProbe,qdpc-host)
endef

define KernelPackage/qts1kpcie/description
 Kernel module for Quantenna support for the R7500
endef

define Build/Compile
	$(MAKE) -C "$(PKG_BUILD_DIR)/../quantenna/pcie2/host/arm" PATH="$(TARGET_PATH)" ARCH="$(LINUX_KARCH)" CROSS_COMPILE="$(TARGET_CROSS)" KERNELDIR="$(LINUX_DIR)" all
endef

define KernelPackage/qts1kpcie/install
	$(INSTALL_DIR) $(1)/lib/modules/$(LINUX_VERSION)
	$(INSTALL_DIR) $(1)/lib/wifi
	$(INSTALL_DIR) $(1)/lib/netifd/wireless
	$(INSTALL_DIR) $(1)/lib/firmware
	$(INSTALL_DATA) ./files/lib/firmware/u-boot.bin $(1)/lib/firmware/u-boot.bin
	$(INSTALL_DATA) ./files/lib/firmware/topaz-linux.lzma.img $(1)/lib/firmware/topaz-linux.lzma.img
	$(INSTALL_BIN) ./files/lib/wifi/qtpcie.sh $(1)/lib/wifi/qtpcie.sh
	$(INSTALL_BIN) ./files/lib/netifd/wireless/qtpcie.sh $(1)/lib/netifd/wireless/qtpcie.sh
endef

$(eval $(call KernelPackage,qts1kpcie))
