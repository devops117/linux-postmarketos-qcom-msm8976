_flavor="postmarketos-qcom-msm8976"
pkgname=linux-$_flavor
pkgver=6.1.0
pkgrel=3
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
_commit="656e89e0017f83ccb1a255a71507d3e9fe7fac1e"
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
b4bd456ead51b949f91951021530d03dfb58be8e82d4ae5355cf63203eb1d9d13c15727a93adfdb68bb865aaf0f2d822df0f2b4db68c24d7e710f48d5ee9d582  linux-postmarketos-qcom-msm8976-656e89e0017f83ccb1a255a71507d3e9fe7fac1e.tar.gz
dd44220e868ae5ea413a3c1fc9afb0dada2f21f56df0710ee43376aff04682019d4c277bfda8e6b7ea30ef4def2ec6223eeddcf708dec35f284ae7bcac5e077b  config-postmarketos-qcom-msm8976.aarch64
"
