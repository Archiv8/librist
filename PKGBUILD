#!/bin/bash

# Maintainer: Daniel Bermond <dbermond@archlinux.org>

pkgname=librist
pkgver=0.2.7
pkgrel=1
pkgdesc="A library that can be used to add the RIST protocol to applications"
arch=("x86_64")
url="https://code.videolan.org/rist/librist/"
license=("BSD")
depends=(
    "cjson"
    "mbedtls"
)
makedepends=(
    "meson"
    "cmake"
    "cmocka"
    "lz4"
)
source=(
    "${pkgname}-${pkgver}"::"https://code.videolan.org/rist/librist/-/archive/v${pkgver}/${pkgname}-v${pkgver}.tar.bz2"
    "010-librist-disable-multicast-tests.patch"
)
sha512sums=(
    "491f3ce0fa7b9698a579caf6c022cf355afdc37da8e00c0c63b49988a830857bd8019ee69b9bd67a035734be4947869085ab797cb625039b50ae601631f3de18"
    "757fc06f1315b3a63d3f9b32ca028edd1243e6e9e7f84c84036786006c73a801dea187e8cefda3936039c44e3b95c59b5cb8923df00e7f3b655e74505eedc7d9"
)

prepare() {
    patch -d "${pkgname}-v${pkgver}" -Np1 -i "${srcdir}/010-librist-disable-multicast-tests.patch"
}

build() {
    arch-meson build "${pkgname}-v${pkgver}"
    ninja -v -C build
}

check() {
    ninja -v -C build test
}

package() {
    DESTDIR="$pkgdir" ninja -v -C build install
    install -D -m644 "${pkgname}-v${pkgver}/COPYING" -t "${pkgdir}/usr/share/licenses/${pkgname}"
}
