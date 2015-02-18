# $Id: PKGBUILD 113973 2014-07-01 10:51:04Z spupykin $
# Maintainer: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Contributor: Dag Odenhall <dag.odenhall@gmail.com>
# Contributor: Grigorios Bouzakis <grbzks@gmail.com>

pkgname=dwm
pkgver=6.0
pkgrel=2
pkgdesc="A dynamic window manager for X"
url="http://dwm.suckless.org"
arch=('i686' 'x86_64')
license=('MIT')
options=(zipman)
depends=('libx11' 'libxinerama')
install=dwm.install
source=(http://dl.suckless.org/dwm/dwm-$pkgver.tar.gz
	config.h
	dwm.desktop
	)
_patches=(
          01-statuscolours.diff
          02-monoclecount.diff
          03-noborder.diff
         )
source=(${source[@]} ${_patches[@]})
md5sums=('8bb00d4142259beb11e13473b81c0857'
         '4228200e2d61ec54d7994684657eff7b'
         '939f403a71b6e85261d09fc3412269ee'
         '57b1a8f21b61c55f906d7cc075111613'
         'e3faeea09a554bbbce29c4d480b0ca41'
         '1f0244803c0188f1b6f4e5794e7f5ca2')

build() {
  cd $srcdir/$pkgname-$pkgver

  for p in "${_patches[@]}"; do
    echo "=> $p"
    patch < ../$p || return 1
  done

  cp $srcdir/config.h config.h
  sed -i 's/CPPFLAGS =/CPPFLAGS +=/g' config.mk
  sed -i 's/^CFLAGS = -g/#CFLAGS += -g/g' config.mk
  sed -i 's/^#CFLAGS = -std/CFLAGS += -std/g' config.mk
  sed -i 's/^LDFLAGS = -g/#LDFLAGS += -g/g' config.mk
  sed -i 's/^#LDFLAGS = -s/LDFLAGS += -s/g' config.mk
  make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11
}

package() {
  cd $srcdir/$pkgname-$pkgver
  make PREFIX=/usr DESTDIR=$pkgdir install
  install -m644 -D LICENSE $pkgdir/usr/share/licenses/$pkgname/LICENSE
  install -m644 -D README $pkgdir/usr/share/doc/$pkgname/README
  install -m644 -D $srcdir/dwm.desktop $pkgdir/usr/share/xsessions/dwm.desktop
}
