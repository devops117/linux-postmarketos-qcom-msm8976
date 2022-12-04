_flavor="postmarketos-qcom-msm8976"
pkgname=linux-$_flavor
pkgver=6.1.0
pkgrel=1
pkgdesc="Mainline kernel fork for Qualcomm MSM8976 devices"
arch="aarch64"
_carch="arm64"
url="https://github.com/Kiciuk/linux"
license="GPL-2.0-only"
options="!strip !check !tracedeps
	pmb:cross-native
	pmb:kconfigcheck-nftables
"
makedepends="
	bison
	findutils
	flex
	openssl-dev
	perl
	postmarketos-installkernel
"

# Source
_repository="linux"
_commit="7108ac91d8225a0c6a39910b66716193f7f56b3f"
source="
	$pkgname-$_commit.tar.gz::https://github.com/Kiciuk/$_repository/archive/$_commit.tar.gz
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
		KBUILD_BUILD_VERSION="$((pkgrel + 1))-$_flavor"
}

package() {
	mkdir -p "$pkgdir"/boot
	make zinstall modules_install dtbs_install \
		ARCH="$_carch" \
		INSTALL_MOD_STRIP=1 \
		INSTALL_PATH="$pkgdir"/boot \
		INSTALL_MOD_PATH="$pkgdir" \
		INSTALL_DTBS_PATH="$pkgdir/usr/share/dtb"

	install -D "$builddir"/include/config/kernel.release \
		"$pkgdir/usr/share/kernel/$_flavor/kernel.release"
}
sha512sums="
c647d0b79c4e23d39684e9bb379d62b0d98e25a1a4516e8ba05ac460c1cdbec29dbf6e1e59080a350d5d310bbffee436c3f554b5e4b18b1ec65eb702b0168a1d  linux-postmarketos-qcom-msm8976-7108ac91d8225a0c6a39910b66716193f7f56b3f.tar.gz
416c0d7b0e20f453235d4160cdf5f31f0dbc6a6a3406775799fae6efbf154eff66d8b5f21a7032e71e5ca53407bda7956e4a59ee116b2dbf6cb977ae57c32110  config-postmarketos-qcom-msm8976.aarch64
"
