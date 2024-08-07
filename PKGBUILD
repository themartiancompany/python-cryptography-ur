# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Maintainer: Felix Yan <felixonmars@archlinux.org>

_py="python"
_pkg=cryptography
pkgname="${_py}-${_pkg}"
pkgver=42.0.6
pkgrel=1
pkgdesc=(
  "A package designed to expose"
  "cryptographic recipes and primitives"
  "to Python developers"
)
pkgdesc="${_pkgdesc[*]}"
arch=(
  'x86_64'
  'arm'
  'aarch64'
  'pentium4'
  'i686'
  'armv7l'
  'mips'
  'powerpc'
)
license=(
  'Apache'
)
url="https://github.com/pyca/${_pkg}"
depends=(
  'python-cffi'
)
makedepends=(
  'clang'
  'git'
  'lld'
  'llvm'
  'python-build'
  'python-installer'
  'python-setuptools-rust'
  'python-wheel'
)
checkdepends=(
  "${_py}-pytest"
  "${_py}-pytest-subtests"
  "${_py}-iso8601"
  "${_py}-pretend"
  "${_py}-hypothesis"
  "${_py}-pytz"
  "${_py}-certifi"
)
source=(
  "git+/${url}.git#tag=${pkgver}"
)
sha512sums=(
  '89b5e3ceffe9d587fc107ff32bce860cd722bf089beec13826f79e3b3799dd4c41d0f074f73c7a43a44b2d58eed6ef0e424d3a8121e2216bd4cf22f737ccb79e'
)

prepare() {
  cd \
    "${_pkg}"
  # Drop all benchmark tests, this means we don't have to checkdepends on pytest-benchmark nor are
  # benchmark tests interesting for a distribution.
  rm -rf tests/bench
}

build() {
  cd \
    "${_pkg}"
  echo $RUSTFLAGS
  # https://github.com/pyca/cryptography/issues/9023
  CC=clang RUSTFLAGS+="-Clinker-plugin-lto -Clinker=clang -Clink-arg=-fuse-ld=lld" python -m build --wheel --no-isolation
}

check() {
  local \
    python_version
  cd \
    "${_pkg}"
  python_version=$( \
    python \
      -c \
      'import sys; print("".join(map(str, sys.version_info[:2])))')
  PYTHONPATH="$PWD/build/lib.linux-${CARCH}-cpython-${python_version}:${PWD}/vectors" \
  pytest -o addopts=''
}

package() {
  cd \
    "${_pkg}"
  "${_py}" \
    -m \
      installer \
    --destdir="${pkgdir}" \
    dist/*.whl
}

