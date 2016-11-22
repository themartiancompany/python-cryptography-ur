# Maintainer: Felix Yan <felixonmars@archlinux.org>

pkgbase=python-cryptography
pkgname=('python-cryptography' 'python2-cryptography')
pkgver=1.6
pkgrel=1
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
source=("https://pypi.io/packages/source/c/cryptography/cryptography-$pkgver.tar.gz")
md5sums=('33ed393be75f04cd889a02a11acbab39')

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
   PYTHONPATH="$PWD/build/lib.linux-$CARCH-3.5:$PYTHONPATH" python setup.py ptr

   cd "$srcdir"/cryptography-$pkgver-python2
   PYTHONPATH="$PWD/build/lib.linux-$CARCH-2.7:$PYTHONPATH" python2 setup.py ptr
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
