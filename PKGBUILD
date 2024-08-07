# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Maintainer: Felix Yan <felixonmars@archlinux.org>

_os="$( \
  uname \
    -o)"
_git=true
[[ "${_os}" == 'Android' ]] && \
  _git=false
_py="python"
_pkg=cryptography
pkgname="${_py}-${_pkg}"
pkgver=43.0.0
pkgrel=1
_pkgdesc=(
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
_http="https://github.com"
_ns="pyca"
url="${_http}/${_ns}/${_pkg}"
depends=(
  "${_py}-cffi"
)
makedepends=(
  'clang'
  'git'
  'lld'
  'llvm'
  "${_py}-build"
  "${_py}-installer"
  "${_py}-setuptools-rust"
  "${_py}-wheel"
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
source=()
sha512sums=()
if [[ "${_git}" == 'true' ]]; then
  source+=(
    "${_pkg}-${pkgver}::git+${url}.git#tag=${pkgver}"
  )
  sha512sums+=(
    '89b5e3ceffe9d587fc107ff32bce860cd722bf089beec13826f79e3b3799dd4c41d0f074f73c7a43a44b2d58eed6ef0e424d3a8121e2216bd4cf22f737ccb79e'
  )
elif [[ "${_git}" == 'false' ]]; then
  source+=(
    "${_pkg}-${pkgver}.tar.gz::${url}/archive/refs/tags/${pkgver}.tar.gz"
  )
  sha512sums+=(
    '3a65539b2f1639d789ea732c6d24d55293c0ca6943c5182d00411fbd1668ab6cac7865f8148bd5f6d4ba676b89780187b77c49da34f4ed34705c94c074037ee7'
  )
fi

prepare() {
  cd \
    "${_pkg}-${pkgver}"
  # Drop all benchmark tests, this means we don't have to checkdepends on pytest-benchmark nor are
  # benchmark tests interesting for a distribution.
  rm \
    -rf \
    tests/bench
}

build() {
  cd \
    "${_pkg}-${pkgver}"
  echo \
    "Rust flags: ${RUSTFLAGS}"
  # https://github.com/pyca/cryptography/issues/9023
  CC=clang \
  RUSTFLAGS+="-Clinker-plugin-lto -Clinker=clang -Clink-arg=-fuse-ld=lld" \
  python \
    -m \
      build \
    --wheel \
    --no-isolation
}

check() {
  local \
    python_version
  cd \
    "${_pkg}-${pkgver}"
  python_version=$( \
    python \
      -c \
      'import sys; print("".join(map(str, sys.version_info[:2])))')
  PYTHONPATH="$PWD/build/lib.linux-${CARCH}-cpython-${python_version}:${PWD}/vectors" \
  pytest -o addopts=''
}

package() {
  cd \
    "${_pkg}-${pkgver}"
  "${_py}" \
    -m \
      installer \
    --destdir="${pkgdir}" \
    dist/*.whl
}

