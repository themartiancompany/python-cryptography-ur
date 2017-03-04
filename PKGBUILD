# Maintainer: Felix Yan <felixonmars@archlinux.org>

pkgbase=python-cryptography
pkgname=('python-cryptography' 'python2-cryptography')
pkgver=1.7.2
pkgrel=2
pkgdesc="A package designed to expose cryptographic recipes and primitives to Python developers"
arch=('i686' 'x86_64')
license=('Apache')
url="http://pypi.python.org/pypi/cryptography"
makedepends=('python-setuptools' 'python2-setuptools' 'python-six' 'python2-six' 'python-cffi'
             'python2-cffi' 'python2-enum34' 'python-pyasn1' 'python2-pyasn1' 'python-idna'
             'python2-idna' 'python2-ipaddress')
checkdepends=('python-pytest-runner' 'python2-pytest-runner' "python-cryptography-vectors=$pkgver"
              "python2-cryptography-vectors=$pkgver" 'python-iso8601' 'python2-iso8601'
              'python-pretend' 'python2-pretend' 'python-pyasn1-modules' 'python2-pyasn1-modules'
              'python-hypothesis' 'python2-hypothesis' 'python-pytz' 'python2-pytz')
source=("https://pypi.io/packages/source/c/cryptography/cryptography-$pkgver.tar.gz"
        32bit-fix.patch::https://github.com/pyca/cryptography/commit/d74ba3298ddd4d3558224af85768e28f4c7f8d0d.patch)
md5sums=('fade66de437392ed1ba6980768626204'
         '9cce8b78c8cc7f532c4f66f2ed116896')

prepare() {
  # https://github.com/pyca/cryptography/issues/3323
  (cd cryptography-$pkgver; patch -p1 -i ../32bit-fix.patch)

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
   depends=('python-pyasn1' 'python-six' 'python-cffi' 'python-idna' 'python-setuptools')

   cd cryptography-$pkgver
   python setup.py install --root="$pkgdir" --optimize=1 --skip-build
}

package_python2-cryptography() {
   depends=('python2-pyasn1' 'python2-six' 'python2-cffi' 'python2-enum34' 'python2-idna'
            'python2-ipaddress' 'python2-setuptools')

   cd cryptography-$pkgver-python2
   python2 setup.py install --root="$pkgdir" --optimize=1 --skip-build
}
