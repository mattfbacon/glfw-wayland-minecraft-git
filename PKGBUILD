# Maintainer: Sven-Hendrik Haase <svenstaro@archlinux.org>
# Contributor: philefou <tuxication AT gmail DOT com>
# Contributor: lindquist <tomas@famolsen.dk>
# Contributor: Christoph Siegenthaler <csi@gmx.ch>
# Contributor: Mihai Militaru <mihai.militaru@ephemeros.org>
# Contributor: SpepS <dreamspepser at yahoo dot it>

pkgbase=glfw
pkgname=('glfw-wayland-minecraft-git')
REV='3fa2360720eeba1964df3c0ecf4b5df8648a8e52'
pkgver="r1.$REV"
pkgrel=1
arch=('x86_64')
url="https://www.glfw.org/"
license=('custom:ZLIB')
makedepends=('mesa' 'cmake' 'doxygen' 'vulkan-headers' 'vulkan-icd-loader'
             'extra-cmake-modules' 'wayland-protocols' 'libxi' 'libxrandr'
             'libxcursor' 'libxkbcommon' 'libxinerama')
source=(
  "$pkgname-$pkgver.tar.gz::https://github.com/glfw/glfw/archive/${REV}.tar.gz"
  "0003-Don-t-crash-on-calls-to-focus-or-icon.patch"
  "0005-Add-warning-about-being-an-unofficial-patch.patch"
)
sha512sums=('21401c38477110a0471deb240b9e459a858b168568ab9d9361f85ec4e5a10ed9417040cdfd185adce543b15870d275aaf1469ba9a351fc007339764b9907587b'
            '8f6e6dd7b5ae8e76ce96c41e6a263262fbefdd4ee43794e28bb62176f06845676e811bb08a213a3f666a10d86b74da19a496622e4665106dab6824cc66db3e6a'
            '997a3cd6470ee958e75422415e7582fb11ffa2e7b718cdf54005e203de480d589f3c49fd88b39b1c8d3c89cc1a9444cdc37b340a797c93fccd20dca0a08da747')

prepare() {
  cd "$srcdir/$pkgbase-$REV"
  mkdir build-wayland

  for patch in "$srcdir/"*.patch; do
    echo "Applying patch $patch"
    patch -p1 < "$patch"
  done
}

build() {
  cd "$srcdir/$pkgbase-$REV/build-wayland"

  cmake .. \
      -DCMAKE_INSTALL_PREFIX=/usr \
      -DCMAKE_INSTALL_LIBDIR=lib \
      -DBUILD_SHARED_LIBS=ON \
      -DGLFW_USE_WAYLAND=ON
}

package_glfw-wayland-minecraft-git() {
  pkgdesc="A free, open source, portable framework for graphical application development (wayland)"
  depends=('wayland' 'libxkbcommon' 'libgl')
  conflicts=('glfw')
  provides=("glfw=$pkgver")

  cd "$srcdir/$pkgbase-$REV"/build-wayland

  make DESTDIR=$pkgdir install

  cd ..
  install -Dm644 LICENSE.md "$pkgdir/usr/share/licenses/$pkgname/LICENSE.md"
}
