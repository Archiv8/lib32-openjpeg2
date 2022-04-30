#!/bin/bash

# Created from the original package by

# Disable various shellcheck rules that produce false positives in this file.
# Repository rules should be added to the .shellcheckrc file located in the
# repository root directory, see https://github.com/koalaman/shellcheck/wiki
# and https://archiv8.github.io for further information.
# shellcheck disable=SC2034,SC2154
# [Query]: Is package still being maintained.  Last release was 3.100, 2017-10-13.  Latest commit was 2021-06-19.
# [ToDo]: Add files: User documentation
# [ToDo]: Add files: Tooling
# [FixMe]: Namcap warnings and errors

# Maintainer: Alexandre Demers <alexandre.f.demers@gmail.com>

_relname=openjpeg2
pkgname="lib32-${_relname}"
pkgver=2.4.0
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
  "55daab47d33823af94e32e5d345b52c251a5410f0c8e0a13b693f17899eedc8b2bb107489ddcba9ab78ef17dfd7cd80d3c5ec80c1e429189cb041124b67e07a8"
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

  # removing unneeded files and folders
  rm -rf "${pkgdir}/usr/"{bin,include}

  # installing license
  mkdir -p "${pkgdir}/usr/share/licenses/${pkgname}/"
  ln -s "/usr/share/licenses/${_relname}/LICENSE" "${pkgdir}/usr/share/licenses/${pkgname}/"
}
