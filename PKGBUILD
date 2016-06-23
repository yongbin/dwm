# $Id: PKGBUILD 165985 2016-03-10 18:31:18Z spupykin $
# Maintainer: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Contributor: Dag Odenhall <dag.odenhall@gmail.com>
# Contributor: Grigorios Bouzakis <grbzks@gmail.com>

pkgname=dwm
pkgver=6.1
pkgrel=3
pkgdesc="A dynamic window manager for X"
url="http://dwm.suckless.org"
arch=('i686' 'x86_64')
license=('MIT')
options=(zipman)
depends=('libx11' 'libxinerama' 'libxft' 'freetype2' 'st' 'dmenu')
install=dwm.install
source=(
  http://dl.suckless.org/dwm/dwm-$pkgver.tar.gz
  config.h
  dwm.desktop
  push.c
)
_patches=(
  06-attachaside.diff
  05-scratchpad.diff
)
source=(${source[@]} ${_patches[@]})
md5sums=('f0b6b1093b7207f89c2a90b848c008ec'
         '69b42a6db274554d81018c80532a8680'
         '939f403a71b6e85261d09fc3412269ee'
         '689534c579b1782440ddcaf71537d8fd'
         '15b1df9b8f74bc84bf3fc1749c160f75'
         '2f5073f9d570c3255a2f60fb27bc49d2')

prepare() {
  cd $srcdir/$pkgname-$pkgver

  for p in "${_patches[@]}"; do
    echo "=> $p"
    patch < ../$p || return 1
  done

  cp $srcdir/config.h config.h
  cp $srcdir/push.c push.c
}

build() {
  cd $srcdir/$pkgname-$pkgver
  make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11 FREETYPEINC=/usr/include/freetype2
}

package() {
  cd $srcdir/$pkgname-$pkgver
  make PREFIX=/usr DESTDIR=$pkgdir install
  install -m644 -D LICENSE $pkgdir/usr/share/licenses/$pkgname/LICENSE
  install -m644 -D README $pkgdir/usr/share/doc/$pkgname/README
  install -m644 -D $srcdir/dwm.desktop $pkgdir/usr/share/xsessions/dwm.desktop
}
