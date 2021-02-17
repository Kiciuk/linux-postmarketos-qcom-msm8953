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
_commit="8502fc0795d8ae89756264352d12f0f846a9f8b4"
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
sha512sums="f9b08004bd9a25c4e9bb952e50a3365ff9a3caea8d680a5c8b3b9c9464a49c93f7b518d7f637dc0224fa1d6a25446624827ad59d4fae29bae2c0bfd138330166  linux-postmarketos-qcom-msm8953-8502fc0795d8ae89756264352d12f0f846a9f8b4.tar.gz
0ceefe3f168855fbd5085b4a8686eea32c5b6610b82ef36e4523fd3c4866f2dbf9f860e54f3e41e08bacbe27456adf0a04f853bc2ce989cd6fc9e0e656315336  config-postmarketos-qcom-msm8953.aarch64"
