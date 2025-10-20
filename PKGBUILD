pkgname=python-gyp
pkgver=20240207.1615ec32
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
    'git'
    'python-build'
    'python-installer'
    'python-setuptools'
    'python-wheel'
)
source=(git+ssh://git@github.com/chromium/gyp#commit=1615ec326858f8c2bd8f30b3a86ea71830409ce4
    0001-Fix-Python-compat-and-remove-six.patch)
sha256sums=(a23ca8b1bf78e1e0fa067d1766241538fd12bd1e6357208ab9eb8ebeed0f0f9e
    2717de3a91cffd5c64cf0cb92bcd587e4d1db7a664ca53bb48efd47b1e57eba7)

pkgver() {
    cd ${pkgname#*-}

    local commit_date="$(TZ=UTC git show -s --pretty=%cd --date=format-local:%Y%m%d HEAD)"
    local short_rev="$(git rev-parse --short HEAD)"

    echo $commit_date.$short_rev
}

prepare() {
    cd ${pkgname#*-}

    git apply -3 ${srcdir}/0001-Fix-Python-compat-and-remove-six.patch
}

build() {
    cd ${pkgname#*-}

    python3 -m build --wheel --no-isolation
}

package() {
    cd ${pkgname#*-}

    python3 -m installer -d ${pkgdir} dist/*.whl
}
