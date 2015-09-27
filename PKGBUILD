# Maintainer: Felix Yan <felixonmars@archlinux.org>

pkgbase=python-cryptography
pkgname=('python-cryptography' 'python2-cryptography')
pkgver=1.0.2
pkgrel=1
pkgdesc="A package designed to expose cryptographic recipes and primitives to Python developers"
arch=('i686' 'x86_64')
license=('Apache')
url="http://pypi.python.org/pypi/cryptography"
makedepends=('python-setuptools' 'python2-setuptools' 'python-six' 'python2-six' 'python-cffi' 'python2-cffi' 'python2-enum34'
             'python-pyasn1' 'python2-pyasn1' 'python-idna' 'python2-idna' 'python2-ipaddress')
checkdepends=('python-pytest' 'python2-pytest' "python-cryptography-vectors=$pkgver" "python2-cryptography-vectors=$pkgver"
              'python-iso8601' 'python2-iso8601' 'python-pretend' 'python2-pretend')
source=("http://pypi.python.org/packages/source/c/cryptography/cryptography-${pkgver}.tar.gz")
md5sums=('6a8627da0c6199fca941dc8170f9b583')

prepare() {
   cp -a cryptography-${pkgver}{,-python2}
}

build() {
   # Build python 3 module
   cd cryptography-${pkgver}
   python3 setup.py build
 
   # Build python 2 module
   cd ../cryptography-${pkgver}-python2
   python2 setup.py build
}

check() {(
   cd "${srcdir}"/cryptography-${pkgver}
   PYTHONPATH="$PWD/build/lib.linux-$CARCH-3.5:$PYTHONPATH" python3 setup.py test

   cd "${srcdir}"/cryptography-${pkgver}-python2
   PYTHONPATH="$PWD/build/lib.linux-$CARCH-2.7:$PYTHONPATH" python2 setup.py test
   ) || warning "Tests failed"
   # Known failure: https://github.com/pyca/cryptography/issues/2354
}
 
package_python-cryptography() {
   depends=('python-pyasn1' 'python-six' 'python-cffi' 'python-idna')
 
   cd cryptography-${pkgver}
   python3 setup.py install --root="${pkgdir}" --optimize=1 --skip-build
}
 
package_python2-cryptography() {
   depends=('python2-pyasn1' 'python2-six' 'python2-cffi' 'python2-enum34' 'python2-idna' 'python2-ipaddress')
 
   cd cryptography-${pkgver}-python2
   python2 setup.py install --root="${pkgdir}" --optimize=1 --skip-build
}
