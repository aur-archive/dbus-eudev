# Maintainer: udeved <udeved@openrc4arch.site40.net>
# Contributor: Tom Gundersen <teg@jklm.no>
# Contributor: Jan de Groot <jgc@archlinux.org>
# Contributor: Link Dupont <link@subpop.net>

 _name="dbus"

pkgname=${_name}-eudev
pkgver=1.8.0
pkgrel=9
pkgdesc="Freedesktop.org message bus system with disabled systemd"
url="http://www.freedesktop.org/Software/dbus"
arch=(i686 x86_64)
license=('GPL' 'custom')
groups=('eudev-base')
depends=('eudev' 'libdbus' 'expat')
makedepends=('libx11' 'xmlto' 'docbook-xsl')
optdepends=('libx11: dbus-launch support'
	    'dbus-openrc: dbus openrc initscript')
provides=('dbus-core' "${_name}")
conflicts=('dbus-core' "${_name}")
replaces=('dbus-core')
options=(!libtool)
source=("http://dbus.freedesktop.org/releases/"${_name}"/"${_name}"-$pkgver.tar.gz"
        '30-dbus')

build() {
  cd dbus-$pkgver
  ./configure \
    --prefix=/usr \
    --sysconfdir=/etc \
    --localstatedir=/var \
    --libexecdir=/usr/lib/dbus-1.0 \
    --with-dbus-user=dbus \
    --with-system-pid-file=/run/dbus/pid \
    --with-system-socket=/run/dbus/system_bus_socket \
    --with-console-auth-dir=/run/console/ \
    --enable-inotify \
    --disable-dnotify \
    --disable-verbose-mode \
    --disable-static \
    --disable-tests  \
    --disable-asserts \
    --disable-systemd
  make
}

package(){
  cd dbus-$pkgver
  make DESTDIR="$pkgdir" install

  rm -rf "$pkgdir/var/run"

  install -Dm755 ${srcdir}/30-dbus "$pkgdir/etc/X11/xinit/xinitrc.d/30-dbus"

  install -Dm644 COPYING "$pkgdir/usr/share/licenses/dbus/COPYING"
  
  rm -r "$pkgdir"/usr/include/dbus-1.0
  rm -r "$pkgdir"/usr/lib/dbus-1.0/include
  rm -r "$pkgdir"/usr/lib/pkgconfig
  rm "$pkgdir"/usr/lib/libdbus-1.so
  rm "$pkgdir"/usr/lib/libdbus-1.so.3
  rm "$pkgdir"/usr/lib/libdbus-1.so.3.8.3
}

sha256sums=('769f8c7282b535ccbe610f63a5f14137a5549834b0b0c8a783e90891b8d70b13'
            'a1c324ae758046f0c3ef46db02ab873d35adeaab9980c2e0ee293accb89d0d2c')
