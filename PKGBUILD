pkgname=dbus
pkgver=1.16.2
pkgrel=1
pkgdesc="Freedesktop.org message bus system"
arch=('x86_64')
url="https://wiki.freedesktop.org/www/Software/dbus/"
license=('GPL-2.0-or-later' 'AFL-2.1')
depends=('expat' 'audit' 'elogind')
makedepends=('meson' 'ninja' 'xmlto' 'docbook-xml' 'docbook-xsl' 'glib2')
provides=('libdbus' 'libdbus-1.so')
source=("https://dbus.freedesktop.org/releases/${pkgname}/${pkgname}-${pkgver}.tar.xz")
sha256sums=('SKIP')

build() {
    meson setup "${srcdir}/${pkgname}-${pkgver}" build \
        --prefix=/usr \
        --sysconfdir=/etc \
        --localstatedir=/var \
        --libexecdir=/usr/lib/dbus-1.0 \
        -Dsystemd=disabled \
        -Duser_session=false \
        -Ddbus_user=root \
        -Dxml_docs=enabled \
        -Dsession_socket_dir=/tmp
    meson compile -C build
}

package() {
    DESTDIR="${pkgdir}" meson install -C build
    rm -rf "${pkgdir}/usr/lib/systemd"
    rm -rf "${pkgdir}/lib/systemd"
    install -d -m 755 "${pkgdir}/etc"
    echo "messagebus:x:18:" >> "${pkgdir}/etc/group"
    echo "messagebus:x:18:18:D-Bus Message Daemon User:/run/dbus:/bin/false" >> "${pkgdir}/etc/passwd"
}
