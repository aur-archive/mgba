# Maintainer: Duck Hunt <vaporeon@tfwno.gf>

pkgbase=mgba
pkgname=('libmgba' 'mgba-qt' 'mgba-sdl')
pkgver=0.1.0
pkgrel=4
pkgdesc="A Nintendo Gameboy Advance Emulator focusing on both speed and accuracy"
arch=('i686' 'x86_64')
url="https://endrift.com/mgba/"
license=('MPL2')
makedepends=('cmake' 'qt5-base' 'sdl2' 'zlib' 'libpng' 'libzip' 'libedit' 'ffmpeg' 'imagemagick')
source=("https://github.com/mgba-emu/mgba/archive/${pkgver}.tar.gz"
        "mgba.desktop")
sha1sums=('a3cefcc31453904a01c5d537b49ed6a62cf6a474'
          '2b6a2c175d01f8ef80ee5d116968866680d033bc')

build() {
  cd "${srcdir}"/mgba-"${pkgver}"/res/
  convert mgba-1024.png -resize 256x256 mgba-256.png
  cd "${srcdir}"/mgba-"${pkgver}"
  mkdir -p build
  cd build
  cmake .. -DCMAKE_INSTALL_PREFIX=/usr
  make
}

package_libmgba() {
  depends=('zlib' 'libpng' 'libzip' 'libedit' 'ffmpeg' 'imagemagick')
  cd "${srcdir}"/mgba-"${pkgver}"/build
  make DESTDIR="${pkgdir}" install
  install -Dm 644 "${srcdir}"/mgba-"${pkgver}"/LICENSE "${pkgdir}"/usr/share/licenses/"${pkgname}"/LICENSE
  rm -rf "${pkgdir}"/usr/bin
}

package_mgba-qt() {
  depends=('libmgba' 'qt5-base' 'sdl2')
  cd "${srcdir}"/mgba-"${pkgver}"/build
  make DESTDIR="${pkgdir}" install
  install -Dm644 "${srcdir}"/mgba-"${pkgver}"/res/mgba-256.png "${pkgdir}"/usr/share/pixmaps/mgba.png
  desktop-file-install "${srcdir}"/mgba.desktop --dir "${pkgdir}"/usr/share/applications/
  rm "${pkgdir}"/usr/bin/mgba
  rm -rf "${pkgdir}"/usr/lib
}

package_mgba-sdl() {
  depends=('libmgba' 'sdl2')
  cd "${srcdir}"/mgba-"${pkgver}"/build
  make DESTDIR="${pkgdir}" install
  rm "${pkgdir}"/usr/bin/mgba-qt
  rm -rf "${pkgdir}"/usr/lib
}
