# Maintainer: Ultracoolguy <myownpersonalaccount@protonmail.com>
# Kernel config based on: arch/arm64/configs/msm8953_defconfig

_flavor="postmarketos-qcom-msm8953"
pkgname=linux-$_flavor
pkgver=5.11_rc6
pkgrel=0
pkgdesc="Mainline kernel fork for Qualcomm MSM8953 devices"
arch="aarch64"
url="https://github.com/msm8953-mainline/linux"
license="GPL-2.0-only"
options="!strip !check !tracedeps pmb:cross-native pmb:kconfigcheck-anbox"
makedepends="bison findutils flex installkernel openssl-dev perl"

_carch="arm64"
# Source
_commit="a737b4b57ee7240880e3e812797cf483a1914037"
source="
	$pkgname-$_commit.tar.gz::https://github.com/Kiciuk/linux/archive/$_commit.tar.gz
	config-$_flavor.$arch
"
builddir="$srcdir/linux-$_commit"

prepare() {
	default_prepare
	cp "$srcdir/config-$_flavor.$arch" .config
}

build() {
	unset LDFLAGS
	make ARCH="$_carch" CC="${CC:-gcc}" \
		KBUILD_BUILD_VERSION=$((pkgrel + 1 ))
}

package() {
	mkdir -p "$pkgdir"/boot
	make zinstall modules_install dtbs_install \
		ARCH="$_carch" \
		INSTALL_PATH="$pkgdir"/boot \
		INSTALL_MOD_PATH="$pkgdir" \
		INSTALL_DTBS_PATH="$pkgdir"/usr/share/dtb
	rm -f "$pkgdir"/lib/modules/*/build "$pkgdir"/lib/modules/*/source

	install -D "$builddir"/include/config/kernel.release \
		"$pkgdir"/usr/share/kernel/$_flavor/kernel.release
}
sha512sums="376ebf41659a8daac823b68642eb3d7f626c7d64e5319157fc645a799e0dea8ec6c3c8105c2a103bb26e37b82d12e80cd853044f1eb5846ad6a1d758d56c410b  linux-postmarketos-qcom-msm8953-a737b4b57ee7240880e3e812797cf483a1914037.tar.gz
fc72028fc130343a40dc3ac9a2f5b1dc2e07729bf847c66cebaa1ebb4dadc2477fba127f6086e58d9b722dfd4a5e1b2224572c9034821268b9a3cce1d66a1ccf  config-postmarketos-qcom-msm8953.aarch64"
