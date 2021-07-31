pkgname=notify-osd-customizable
_realname=notify-osd
pkgver=0.9.35
pkgrel=6
_realver=${pkgver}+16.04.20160415
pkgdesc="daemon that displays passive pop-up notifications, with leolik patch added"
arch=(i686 x86_64)
url="https://github.com/uttarayan21/notify-osd-customizable"
license=('GPL')
groups=()
depends=('libwnck3' 'libnotify>=0.7.0' 'dbus-glib>=0.76' 'dconf' 'gsettings-desktop-schemas')
optdepends=('notifyconf: gui to customize notifies appearence')
makedepends=('pkgconfig' 'libnotify' 'gnome-common')
provides=('notification-daemon' 'notify-osd')
conflicts=('notify-osd')
install=$pkgname.install
source=("$pkgname::git+${url}.git")

build() {
  cd "$srcdir/$_realname-$_realver"
  #sed -i 's,/usr/lib/notify-osd/,@LIBEXECDIR@/,' data/org.freedesktop.Notifications.service.in

  export AUTOMAKE=automake
  sh ./autogen.sh --prefix=/usr --sysconfdir=/etc --localstatedir=/var --libexecdir=/usr/lib/$pkgname \
              --disable-static --disable-schemas-compile
 
  make || return 1
 }

package() {
	cd "$srcdir/$_realname-$_realver"
	make DESTDIR="$pkgdir/" install
	install -D -m644 ${srcdir}/config ${pkgdir}/etc/skel/.config/notify-osd/config
 }

