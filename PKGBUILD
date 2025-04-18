# Maintainer: Nikolaos Bezirgiannis <bezeria@gmail.com>
# Contributor: Alexander Rødseth <rodseth@gmail.com>
# Contributor: Jachym Barvinek <jachymb@gmail.com>
# Contributor: Thomas Dziedzic < gostrc at gmail >
# Contributor: John Proctor <jproctor@prium.net>
# Contributor: Juergen Hoetzel <juergen@archlinux.org>

pkgname=swi-prolog7
pkgver=7.6.4
pkgrel=1
pkgdesc='Prolog environment (latest git stable version)'
arch=('x86_64' 'i686' 'aarch64')
url='http://www.swi-prolog.org/'
license=('GPL' 'LGPL')
depends=('gmp' 'readline' 'openssl' 'libarchive')
makedepends=('git' 'libxft' 'libjpeg' 'unixodbc' 'libxpm' 'libxinerama')
optdepends=('unixodbc: for using the odbc4pl library'
            'libjpeg: for using the pl2xpce library'
            'libxpm: for using the pl2xpce library'
            'libxinerama: for using the pl2xpce library'
            'libxft: for using the pl2xpce library'
            'java-environment: for interfacing java with the jpl package')
#options=('!makeflags')
source=("https://github.com/SWI-Prolog/swipl/archive/refs/tags/V$pkgver.tar.gz"
    '0001-The-test-may-fail-due-to-default-CFLAGS.patch'
)
sha256sums=('02fa31f0cd587deda6f3446e2e045aa45afe3d845834fb295ae8eb535bfdc533'
    '5527f05f9cb1fa7fe111edea1bb1b9869fbfa8025f3c6ad74f7d9e9e802c8a4d'
)
conflicts=('swi-prolog')

prepare() {
    cd "${srcdir}/swipl-$pkgver"
    patch -p1 --input="${srcdir}/0001-The-test-may-fail-due-to-default-CFLAGS.patch"
}


build() {
  cd "${srcdir}/swipl-$pkgver/src/"
  echo "warn" > .doc-action

  autoheader
  autoconf

  ./configure --prefix=/usr \
    --disable-static        \
    --enable-shared         \
    ax_cv_c_float_words_bigendian=no
   make
}

package() {
  cd "${srcdir}/swipl-$pkgver/src/"
  make DESTDIR="$pkgdir" install

  # Fix for FS#20873
  chmod +x "$pkgdir/usr/lib/swipl-${pkgver}/library/dialect/sicstus/swipl-lfr.pl"
}

