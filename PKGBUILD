# $Id$
# Maintainer: AndyRTR <andyrtr@archlinux.org>
# Contributor: Alexander Fehr <pizzapunk gmail com>

pkgname=hunspell-de-base
pkgver=20131206
pkgrel=1
pkgdesc="German hunspell dictionaries. No symlink (de_BE, de_LI and de_LU)"
arch=('any')
url="http://www.j3e.de/ispell/igerman98/"
license=('GPL' 'custom:OASIS')
makedepends=('ispell')
optdepends=('hunspell: the spell checking libraries and apps')
provides=('hunspell-de')
conflicts=('hunspell-de')
source=("http://www.j3e.de/ispell/igerman98/dict/igerman98-$pkgver.tar.bz2")
md5sums=('9b6c0c6615d2e099cd85a209d9f1fdbb')

build() {
  cd "$srcdir/igerman98-$pkgver"
  make hunspell/de_AT.dic hunspell/de_AT.aff \
       hunspell/de_CH.dic hunspell/de_CH.aff \
       hunspell/de_DE.dic hunspell/de_DE.aff
}

package() {
  cd "$srcdir/igerman98-$pkgver/hunspell"
  install -dm755 ${pkgdir}/usr/share/hunspell
  cp -p de_??.dic de_??.aff $pkgdir/usr/share/hunspell

  pushd $pkgdir/usr/share/hunspell/
  popd

  # the symlinks
  install -dm755 ${pkgdir}/usr/share/myspell/dicts
  pushd $pkgdir/usr/share/myspell/dicts
    for file in $pkgdir/usr/share/hunspell/*; do
      ln -sv /usr/share/hunspell/$(basename $file) .
    done
  popd

  # docs
  install -dm755 ${pkgdir}/usr/share/doc/$pkgname
  cp -p README_de_??.txt $pkgdir/usr/share/doc/$pkgname

  # licenses
  install -D -m644 Copyright $pkgdir/usr/share/licenses/$pkgname/Copyright
  install -D -m644 COPYING_OASIS $pkgdir/usr/share/licenses/$pkgname/COPYING_OASIS
}
