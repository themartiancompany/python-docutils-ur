# Maintainer: Sébastien Luttringer <seblu@aur.archlinux.org>
# Contributor : Ionut Biru <ibiru@archlinux.org>
# Contributor: Sergej Pupykin <pupykin.s+arch@gmail.com>

pkgname=python-docutils
pkgver=0.8.1
pkgrel=1
pkgdesc='Set of tools for processing plaintext docs into formats such as HTML, XML, or LaTeX'
arch=('any')
url='http://docutils.sourceforge.net'
license=('custom')
depends=('python')
conflicts=('docutils')
#provides=("docutils=$pkgver")
source=("http://downloads.sourceforge.net/docutils/docutils-$pkgver.tar.gz")
md5sums=('2ecf8ba3ece1be1ed666150a80c838c8')

build() {
  cd docutils-$pkgver
  python setup.py build
}

package() {
  cd docutils-$pkgver
  python setup.py install --root="$pkgdir" --optimize=1

  for f in "$pkgdir"/usr/bin/*.py; do
      ln -s "$(basename $f)" "$pkgdir/usr/bin/$(basename $f .py)"
  done

  install -D -m644 COPYING.txt "$pkgdir/usr/share/licenses/$pkgname/COPYING.txt"
  install -D -m644 licenses/python* "$pkgdir/usr/share/licenses/$pkgname/"
}

# vim:set ts=2 sw=2 ft=sh et:
