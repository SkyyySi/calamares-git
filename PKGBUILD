# Maintainer: SkyyySi

pkgname=calamares-git
_pkgname=calamares
pkgver=3.2.32.1.r33.gf629826d4
pkgrel=1
pkgdesc='Distribution-Independent Installer Framework'
arch=('i686' 'x86_64')
license=('GPL3')
url='https://github.com/calamares/calamares'
provides=('calamares')
conflicts=('calamares')
depends=('kconfig'
         'kcoreaddons'
         'kiconthemes'
         'ki18n'
         'kio'
         'solid'
         'yaml-cpp'
         'kpmcore>=4.1.0'
         'boost'
         'boost-libs'
         'hwinfo'
         'qt5-svg'
         'polkit-qt5'
         'gtk-update-icon-cache'
         'plasma-framework'
         'qt5-xmlpatterns'
         'squashfs-tools'
         'libpwquality'
         'appstream-qt'
)
source=(
        "$_pkgname::git+$url"
        "20-nopasswd-calamares.rules"
)
sha256sums=(
            "SKIP"
            "c9b7cae731437bad71c1387543d85cf658ed14fd112bec003d1b0e28d7e5a364"
)

pkgver() {
	cd "$srcdir/$_pkgname"
	git describe --long --tags | sed 's/^v//;s/\([^-]*-g\)/r\1/;s/-/./g'
}

build() {
	cd ${srcdir}/calamares
	mkdir -p build && cd build
	cmake .. -DCMAKE_INSTALL_PREFIX=/usr
	make
}

package() {
	cd ${srcdir}/calamares/build
	make DESTDIR="$pkgdir" install
	install -Dm644 "$srcdir/20-nopasswd-calamares.rules" "$pkgdir/etc/polkit-1/rules.d/20-nopasswd-calamares.rules"
}
