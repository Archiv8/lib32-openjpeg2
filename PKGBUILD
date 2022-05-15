#!/bin/bash

# Created from the original package by Alexandre Demers <alexandre.f.demers@gmail.com>

# Disable various shellcheck rules that produce false positives in this file.
# Repository rules should be added to the .shellcheckrc file located in the
# repository root directory, see https://github.com/koalaman/shellcheck/wiki
# and https://archiv8.github.io for further information.
# shellcheck disable=SC2034,SC2154
# [ToDo]: Add files: User documentation
# [ToDo]: Add files: Tooling
# [FixMe]: Namcap warnings and errors

# Maintainer: Ross Clark <https://github.com/Archiv8/lib32-openjpeg2/discussions>
# Contributor: Ross Clark <https://github.com/Archiv8/lib32-openjpeg2/discussions>

_relname=openjpeg2

pkgname="lib32-${_relname}"
pkgver=2.5.0
pkgrel=1
pkgdesc="An open source JPEG 2000 codec, version ${pkgver}"
arch=("x86_64")
license=("BSD")
url="http://www.openjpeg.org"
makedepends=(
  "cmake"
  "lib32-libpng"
  "lib32-libtiff"
  "lib32-lcms2"
)
depends=(
  "${_relname}=${pkgver}"
  "lib32-gcc-libs"
  "lib32-zlib"
)
source=(
  "https://github.com/uclouvain/openjpeg/archive/v${pkgver}.tar.gz"
)
sha512sums=(
  "08975a2dd79f1e29fd1824249a5fbe66026640ed787b3a3aa8807c2c69f994240ff33e2132f8bf15bbc2202bef7001f98e42d487231d4eebc8e503538658049a"
)

prepare() {
  mkdir -p build

  # Patching if needed
}


build() {
  export CFLAGS="-m32"
  export CXXFLAGS="-m32"
  export PKG_CONFIG_PATH="/usr/lib32/pkgconfig"

  cd build

  cmake "../openjpeg-$pkgver" \
    -DCMAKE_BUILD_TYPE=Release \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -DOPENJPEG_INSTALL_LIB_DIR=lib32 \
    -DBUILD_SHARED_LIBS=ON \
    -DBUILD_STATIC_LIBS=OFF \
    -DBUILD_DOC=off
  make
}

package() {
  make -C build DESTDIR="${pkgdir}" install

  # Remove unwanted files and folders, including those that may clash with openjpeg2
  rm -rf "${pkgdir}/usr/"{bin,include}

  # Install license
  mkdir -p "${pkgdir}/usr/share/licenses/${pkgname}/"
  ln -s "/usr/share/licenses/${_relname}/LICENSE" "${pkgdir}/usr/share/licenses/${pkgname}/"
}
