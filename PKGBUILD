# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Maintainer: Daniel M. Capella <polyzen@archlinux.org>
# Contributor: Sébastien Luttringer
# Contributor : Ionut Biru <ibiru@archlinux.org>
# Contributor: Sergej Pupykin <pupykin.s+arch@gmail.com>

_py="python"
_pyver="$( \
  "${_py}" \
    -V | \
    awk \
      '{print $2}')"
_pymajver="${_pyver%.*}"
_pyminver="${_pymajver#*.}"
_pynextver="${_pymajver%.*}.$(( \
  ${_pyminver} + 1))"
_pkg=docutils
pkgname="${_py}-${_pkg}"
pkgver=0.21.2
pkgrel=1
epoch=1
_pkgdesc=(
  'Set of tools for processing plaintext'
  "docs into formats such as HTML, XML, or LaTeX"
)
pkgdesc="${_pkgdesc[*]}"
arch=(
  'any'
)
url="http://${_pkg}.sourceforge.net"
license=(
  'custom'
)
depends=(
  "${_py}>=${_pymajver}"
  "${_py}<${_pynextver}"
)
makedepends=(
  "${_py}-build"
  "${_py}-flit-core"
  "${_py}-installer"
)
checkdepends=(
  "${_py}-pillow"
)
optdepends=(
  "${_py}-myst-parser: to parse input in 'Markdown' (CommonMark) format"
  "${_py}-pillow: for some image manipulation operations"
  "${_py}-pygments: for syntax highlighting of code directives and roles"
)
_sf="https://downloads.sourceforge.net"
source=(
  "${_sf}/${_pkg}/${_pkg}-$pkgver.tar.gz"
)
b2sums=(
  '727c2f97fc5835a0ffa62e38ea85af366cd89ad1eaec0b8af8b1f3b12e6cddfddb65161ba34f9109952d37ba2cf8985f3c3b6905ebb2ac1c9a984cce3fb4d170'
)

prepare() {
  cd \
    "${_pkg}-${pkgver}"
  # Remove include list
  # https://github.com/pypa/wheel/issues/92
  sed \
    -i \
    '/^include =/,/]/d' \
    pyproject.toml
}

build() {
  cd \
    "${_pkg}-${pkgver}"
  "${_py}" \
    -m \
      build \
    --wheel \
    --skip-dependency-check \
    --no-isolation
}

check() {
  cd \
    "${_pkg}-${pkgver}"
  # we need utf locale to valid utf8 tests
  export \
    LANG=en_US.UTF-8
  PYTHONPATH="$PWD/build/python/" \
  "${_py}" \
    test/alltests.py
}

package() {
  local \
    _site_packages
  _site_packages=$( \
    "${_py}" \
      -c \
        "import site; print(site.getsitepackages()[0])")
  cd \
    "${_pkg}-${pkgver}"
  "${_py}" \
    -m \
      installer \
      --destdir="${pkgdir}" \
      dist/*.whl
  # symlink license file
  install \
    -d \
    "${pkgdir}/usr/share/licenses/${pkgname}"
  ln \
    -s \
    "${_site_packages}/${_pkg}-${pkgver}.dist-info/COPYING.txt" \
    "${pkgdir}/usr/share/licenses/${pkgname}/COPYING.txt"
}

# vim:set ts=2 sw=2 et:
