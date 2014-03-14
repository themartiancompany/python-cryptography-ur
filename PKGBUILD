# Maintainer: Felix Yan <felixonmars@gmail.com>

pkgbase=python-cryptography
pkgname=('python-cryptography' 'python2-cryptography')
pkgver=0.2.2
pkgrel=1
pkgdesc="A package designed to expose cryptographic recipes and primitives to Python developers"
arch=('i686' 'x86_64')
license=('Apache')
url="http://pypi.python.org/pypi/cryptography"
makedepends=('python-setuptools' 'python2-setuptools' 'python-six' 'python2-six' 'python-cffi' 'python2-cffi')
checkdepends=('python-pytest' 'python2-pytest')
source=("http://pypi.python.org/packages/source/c/cryptography/cryptography-${pkgver}.tar.gz")
md5sums=('f002a442c8c5c7463bf8d2f11f6c3128')

check() {
   # Check python3 module
   cd "${srcdir}"/cryptography-${pkgver}
   python3 setup.py test

   # Check python2 module
   cd "${srcdir}"/cryptography-${pkgver}-python2
   python2 setup.py test
}
 
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
 
package_python-cryptography() {
   depends=('python' 'python-six' 'python-cffi')
 
   cd cryptography-${pkgver}
   python3 setup.py install --root="${pkgdir}" --optimize=1 --skip-build
}
 
package_python2-cryptography() {
   depends=('python2' 'python2-six' 'python2-cffi')
 
   cd "${srcdir}/cryptography-${pkgver}-python2"
   python2 setup.py install --root="${pkgdir}" --optimize=1 --skip-build
}
