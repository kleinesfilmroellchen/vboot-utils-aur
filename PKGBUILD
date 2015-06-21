# Maintainer: Anatol Pomozov <anatol.pomozov@gmail.com>
# Contributor: Thomas Sowell <tom@fancydriving.org>

pkgname=vboot-utils
pkgdesc='Chromium OS verified boot utilities'
pkgver=44.7077
_tag=release-R${pkgver/\./-}.B
pkgrel=1
arch=(i686 x86_64)
url='https://chromium.googlesource.com/chromiumos/platform/vboot_reference'
license=('custom:chromiumos')
depends=(libutil-linux openssl)
makedepends=(libyaml trousers)
source=(https://chromium.googlesource.com/chromiumos/platform/vboot_reference/+archive/refs/heads/$_tag.tar.gz)
sha1sums=('791308e35dc867ec33879dd7add9c1eb3a22c7b1')

build() {
  make
}

check() {
  make runtests
}

package() {
  make DESTDIR="$pkgdir" MINIMAL=1 install
  install -d "$pkgdir"/usr/share/vboot/
  cp -r tests/devkeys "$pkgdir"/usr/share/vboot/devkeys
  install -m 644 -D LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
}
