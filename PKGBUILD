# Maintainer: Benjamin Levy <blevy@protonmail.com>

pkgname=cmatrix-git
pkgver=1.2.r108.g0365a63
pkgrel=1
pkgdesc="A curses-based scrolling 'Matrix'-like screen"
arch=('x86_64')
url="http://www.asty.org/cmatrix/"
license=('GPL3')
depends=('ncurses')
makedepends=('fontconfig')
optdepends=('fontconfig: custom font')
conflicts=('cmatrix')
provides=('cmatrix')
source=("git+https://github.com/abishekvashok/cmatrix"
        "0001-Fix-unicode-character-printing.patch")
md5sums=('SKIP'
         '8eff5e9b5f83f5bd2691f26452820b36')

pkgver() {
  cd "$srcdir/cmatrix"
  git describe --long --tags | sed 's/^v//;s/\([^-]*-g\)/r\1/;s/-/./g'
}

prepare() {
    cd "$srcdir/cmatrix"
    patch --forward --strip=1 --input="${srcdir}/0001-Fix-unicode-character-printing.patch"
}

build() {
  cd "cmatrix"

  autoreconf -i
  CPPFLAGS="-D_FORTIFY_SOURCE=0" ./configure \
    --prefix=/usr --mandir=/usr/share/man

  make
}

package() {
  cd "cmatrix"

  install -d "$pkgdir/usr/share/fonts/misc/"
  install -d "$pkgdir/usr/share/kbd/consolefonts/"
  make DESTDIR="$pkgdir" install

  rm -f "$pkgdir/usr/share/fonts/misc/fonts.dir"

  for i in AUTHORS NEWS COPYING README ChangeLog INSTALL; do
    install -Dm644 $i "$pkgdir/usr/share/doc/cmatrix/$i"
  done
}
