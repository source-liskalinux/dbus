pkgname=dbus
pkgver=1.16.2
pkgrel=1
pkgdesc="Freedesktop.org message bus system (without systemd)"
arch=('x86_64')
url="https://wiki.freedesktop.org/www/Software/dbus/"
license=('GPL-2.0-or-later' 'AFL-2.1')
depends=('expat' 'audit' 'elogind')
makedepends=('cmake' 'ninja' 'xmlto' 'docbook-xml' 'docbook-xsl')
provides=('dbus' 'libdbus-1.so')
conflicts=('dbus-systemd')
source=("https://dbus.freedesktop.org/releases/${pkgname}/${pkgname}-${pkgver}.tar.xz")
sha256sums=('SKIP')

build() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  cmake -B build -G Ninja \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -DCMAKE_INSTALL_SYSCONFDIR=/etc \
    -DCMAKE_INSTALL_LOCALSTATEDIR=/var \
    -DCMAKE_INSTALL_LIBDIR=lib \
    -DDBUS_ENABLE_SYSTEMD=OFF \
    -DDBUS_ENABLE_XML_DOCS=ON \
    -DDBUS_SESSION_SOCKET_DIR=/tmp \
    -DCMAKE_POLICY_VERSION_MINIMUM=3.5
  cmake --build build
}

package() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  DESTDIR="${pkgdir}" cmake --install build
  rm -rf "${pkgdir}/usr/lib/systemd"
  rm -rf "${pkgdir}/lib/systemd"
}
