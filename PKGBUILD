# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Maintainer: George Rawlinson <grawlinson@archlinux.org>
# Contributor: Eli Schwartz <eschwartz@archlinux.org>

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
_pkg=distlib
_pkgname="${_pkg}"
pkgname="${_py}-${_pkg}"
pkgver=0.3.8
pkgrel=1
_pkgdesc=(
  'Low-level functions that relate to packaging'
  'and distribution of Python software'
)
arch=(
  'any'
)
url="https://${_pkg}.readthedocs.io"
license=(
  'PSF'
)
depends=(
  "${_py}>=${_pymajver}"
  "${_py}<${_pynextver}"
)
makedepends=(
  'git'
  "${_py}-build"
  "${_py}-installer"
  "${_py}-setuptools"
  "${_py}-wheel"
)
_commit='ab5f8e797fbc56a0e3488bba68d05e7a602cb63f'
_http="https://github.com"
_ns="vsajip"
_url="${_http}/${_ns}/${_pkg}"
source=(
  "${_pkg}::git+${_url}#commit=${_commit}"
)
b2sums=(
  'SKIP'
)

pkgver() {
  cd \
    "${_pkg}"
  git \
    describe \
    --tags | \
    sed \
      's/^v//'
}

prepare() {
  cd \
    "${_pkg}"
  # do not bundle executables of unknown provenance
  rm \
    "distlib/"*".exe"
}

build() {
  cd \
    "${_pkg}"
  "${_py}" \
    -m \
      build \
    --wheel \
    --no-isolation
}

check() {
  cd \
    "${_pkg}"
  "${_py}" \
    "tests/test_all.py"
}

package() {
  cd \
    "${_pkg}"
  "${_py}" \
    -m \
      installer \
    --destdir="${pkgdir}" \
    "dist/"*".whl"
}
