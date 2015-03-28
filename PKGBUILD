# Maintainer: Felix Yan <felixonmars@archlinux.org>

pkgbase=python-cryptography
pkgname=('python-cryptography' 'python2-cryptography')
pkgver=0.8.1
pkgrel=2
pkgdesc="A package designed to expose cryptographic recipes and primitives to Python developers"
arch=('i686' 'x86_64')
license=('Apache')
url="http://pypi.python.org/pypi/cryptography"
makedepends=('python-setuptools' 'python2-setuptools' 'python-six' 'python2-six' 'python-cffi' 'python2-cffi' 'python2-enum34'
             'python-pyasn1' 'python2-pyasn1')
checkdepends=('python-pytest' 'python2-pytest' 'python-cryptography-vectors' "python2-cryptography-vectors=$pkgver"
              'python-iso8601' 'python2-iso8601' 'python-pretend' 'python2-pretend')
source=("http://pypi.python.org/packages/source/c/cryptography/cryptography-${pkgver}.tar.gz")
md5sums=('70dde78a5515abdbfd7a3d58f15689ab')

prepare() {
   cp -a cryptography-${pkgver}{,-python2}

   # Don't depend on enum34 since we already have python 3.4
   sed -i 's/"enum34",//' cryptography-${pkgver}/setup.py
}

build() {
   # Build python 3 module
   cd cryptography-${pkgver}
   python3 setup.py build
 
   # Build python 2 module
   cd ../cryptography-${pkgver}-python2
   python2 setup.py build
}

check() {
   # Check python3 module
   cd "${srcdir}"/cryptography-${pkgver}
   PYTHONPATH="$(pwd)/build/lib.linux-$CARCH-3.4:$PYTHONPATH" python3 setup.py test

   # Check python2 module
   cd "${srcdir}"/cryptography-${pkgver}-python2
   PYTHONPATH="$(pwd)/build/lib.linux-$CARCH-2.7:$PYTHONPATH" python2 setup.py test
}
 
package_python-cryptography() {
   depends=('python-pyasn1' 'python-six' 'python-cffi')
 
   cd cryptography-${pkgver}
   python3 setup.py install --root="${pkgdir}" --optimize=1 --skip-build
}
 
package_python2-cryptography() {
   depends=('python2-pyasn1' 'python2-six' 'python2-cffi' 'python2-enum34')
 
   cd cryptography-${pkgver}-python2
   python2 setup.py install --root="${pkgdir}" --optimize=1 --skip-build
}
