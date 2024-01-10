# Maintainer: Anatol Pomozov <anatol.pomozov@gmail.com>
# Contributor: Thomas Sowell <tom@fancydriving.org>

pkgname=vboot-utils
pkgdesc='Chromium OS verified boot utilities'
pkgver=112.15359
_tag=release-R${pkgver/\./-}.B
pkgrel=1
arch=(i686 x86_64)
url='https://chromium.googlesource.com/chromiumos/platform/vboot_reference'
license=('custom:chromiumos')
depends=(libutil-linux openssl libzip flashrom-git)
makedepends=(git libyaml trousers)
source=(git+https://chromium.googlesource.com/chromiumos/platform/vboot_reference#branch=$_tag
        disable-errors.patch
        use-sensible-test-pointer.patch)
sha256sums=('SKIP'
            '8c59c1fdc2b8cd0e76b2b9f1001a6ce611aa1e011fa88d6055c9578a089cc1fc'
            '017b034e4d5dba3dbe2aeda920aa15cfa4fb64a1344aed410fa6113e13b19a24')

prepare() {
  cd vboot_reference
  patch -p1 < ../disable-errors.patch
  patch -p1 < ../use-sensible-test-pointer.patch
}

build() {
  cd vboot_reference
  make
}

check() {
  cd vboot_reference
  make runtests || true
}

package() {
  cd vboot_reference
  make install DESTDIR="$pkgdir" MINIMAL=1
  install -d "$pkgdir"/usr/share/vboot/
  cp -r tests/devkeys "$pkgdir"/usr/share/vboot/devkeys
  install -m 644 -D LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
}
