# Maintainer: Felix Yan <felixonmars@archlinux.org>

pkgbase=python-cryptography
pkgname=('python-cryptography' 'python2-cryptography')
pkgver=1.9
pkgrel=1
pkgdesc="A package designed to expose cryptographic recipes and primitives to Python developers"
arch=('i686' 'x86_64')
license=('Apache')
url="http://pypi.python.org/pypi/cryptography"
makedepends=('python-setuptools' 'python2-setuptools' 'python-six' 'python2-six' 'python-cffi'
             'python2-cffi' 'python2-enum34' 'python-pyasn1' 'python2-pyasn1' 'python-idna'
             'python2-idna' 'python2-ipaddress' 'python-asn1crypto' 'python2-asn1crypto')
checkdepends=('python-pytest-runner' 'python2-pytest-runner' "python-cryptography-vectors=$pkgver"
              "python2-cryptography-vectors=$pkgver" 'python-iso8601' 'python2-iso8601'
              'python-pretend' 'python2-pretend' 'python-hypothesis' 'python2-hypothesis'
              'python-pytz' 'python2-pytz')
source=("https://pypi.io/packages/source/c/cryptography/cryptography-$pkgver.tar.gz")
sha512sums=('815e9c09366935f8603a3e6e74c28ce79175596d00dbcd19d3792505237bd1cf953a4f401c2b97e4beaa7f2bbdcf9d7f95c4753d001a07fa816830af97cdd24e')

prepare() {
  cp -a cryptography-${pkgver}{,-python2}
}

build() {
  cd "$srcdir"/cryptography-$pkgver
  python setup.py build

  cd "$srcdir"/cryptography-$pkgver-python2
  python2 setup.py build
}

check() {
  cd "$srcdir"/cryptography-$pkgver
  python setup.py pytest

  cd "$srcdir"/cryptography-$pkgver-python2
  python2 setup.py pytest
}

package_python-cryptography() {
  depends=('python-six' 'python-cffi' 'python-idna' 'python-setuptools' 'python-asn1crypto')

  cd cryptography-$pkgver
  python setup.py install --root="$pkgdir" --optimize=1 --skip-build
}

package_python2-cryptography() {
  depends=('python2-six' 'python2-cffi' 'python2-enum34' 'python2-idna' 'python2-ipaddress'
           'python2-setuptools' 'python2-asn1crypto')

  cd cryptography-$pkgver-python2
  python2 setup.py install --root="$pkgdir" --optimize=1 --skip-build
}
