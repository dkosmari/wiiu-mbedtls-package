_realname=mbedtls
pkgname=wiiu-${_realname}
pkgver=3.6.4
pkgrel=2
pkgdesc='An open source, portable, easy to use, readable and flexible SSL library'
arch=('any')
url='https://tls.mbed.org'
license=('Apache-2.0', 'GPL-2.0-or-later')
options=(!strip libtool staticlibs)
makedepends=('wiiu-cmake' 'wiiu-pkg-config' 'dkp-toolchain-vars')
groups=('wiiu-portlibs')

source=(
  "${_realname}-${pkgver}.tar.bz2::https://github.com/Mbed-TLS/${_realname}/releases/download/${_realname}-${pkgver}/${_realname}-${pkgver}.tar.bz2"
  "wiiu-mbedtls-${pkgver}.patch"
)

build() {
  cd ${_realname}-${pkgver}

  patch -Np1 -i $srcdir/wiiu-${_realname}-${pkgver}.patch

  CMAKE_C_COMPILER_LAUNCHER=ccache \
  CMAKE_CXX_COMPILER_LAUNCHER=ccache \
  /opt/devkitpro/portlibs/wiiu/bin/powerpc-eabi-cmake \
    -DCMAKE_INSTALL_PREFIX=/opt/devkitpro/portlibs/wiiu \
    -DCMAKE_BUILD_TYPE=Release \
    -DENABLE_TESTING=Off \
    -DENABLE_PROGRAMS=Off \
    .

  make
}

package() {
  cd ${_realname}-${pkgver}

  source ${DEVKITPRO}/wiiuvars.sh

  make install DESTDIR="$pkgdir"

  install -Dm644 LICENSE "${pkgdir}/${PORTLIBS_PREFIX}/licenses/${pkgname}/LICENSE"
}

sha256sums=('ec35b18a6c593cf98c3e30db8b98ff93e8940a8c4e690e66b41dfc011d678110'
            'f01a065d6e6d2fcbf0a710b4bbe2305fec6c7f4489b3695ad326f2593b7dea1f')
