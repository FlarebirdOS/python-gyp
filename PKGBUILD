pkgname=python-gyp
pkgver=20240207.1615ec32
_commit=1615ec326858f8c2bd8f30b3a86ea71830409ce4
pkgrel=1
pkgdesc="Generate Your Projects meta-build system"
arch=('x86_64')
url="https://gyp.gsrc.io"
license=('BSD-3-Clause')
depends=(
    'ninja'
    'python'
)
makedepends=(
    'python-build'
    'python-installer'
    'python-setuptools'
    'python-wheel'
)
source=(https://github.com/chromium/gyp/archive/${pkgname#*-}-${_commit}.tar.gz
    0001-Fix-Python-compat-and-remove-six.patch)
sha256sums=(b0a624cebe7e7d0f532532e73d132fabbd9246dc7a52e8e62cfe214a2e32da26
    2717de3a91cffd5c64cf0cb92bcd587e4d1db7a664ca53bb48efd47b1e57eba7)

prepare() {
    cd ${pkgname#*-}-${_commit}

    patch -Np1 -i ${srcdir}/0001-Fix-Python-compat-and-remove-six.patch
}

build() {
    cd ${pkgname#*-}-${_commit}

    python3 -m build --wheel --skip-dependency-check --no-isolation
}

package() {
    cd ${pkgname#*-}-${_commit}

    python3 -m installer -d ${pkgdir} dist/*.whl
}
