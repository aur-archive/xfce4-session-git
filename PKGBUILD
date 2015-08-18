# $Id
# Maintainer:  Silvio Knizek <killermoehre@gmx.net>
# Contributor: Evangelos Foutras <evangelos@foutrelis.com>
# Contributor: Diego Principe <cdprincipeat gmaildot com>
# Contributor: Baurzhan Muftakhidinov <baurthefirst@gmail.com>
# Contributor: Pablo Lezaeta <prflr@gmail.com>

_pkgname=xfce4-session
pkgname="${_pkgname}-git"
pkgver=4.12.0.r15.g0419797
pkgrel=1
pkgdesc="A session manager for Xfce"
arch=('i686' 'x86_64')
url="http://www.xfce.org/"
license=('GPL2')
groups=('xfce4')
depends=('libxfce4ui' 'libwnck' 'libsm' 'polkit' 'xorg-iceauth' 'xorg-xinit'
         'xorg-xrdb' 'polkit-gnome' 'hicolor-icon-theme')
makedepends=('intltool' 'git' 'xfce4-dev-tools')
optdepends=('gnome-keyring: for keyring support when GNOME compatibility is enabled'
            'light-locker: for locking screen with xflock4 (suggested)'
            'xscreensaver: for locking screen with xflock4'
            'gnome-screensaver: for locking screen with xflock4'
            'xlockmore: for locking screen with xflock4'
            'slock: for locking screen with xflock4')
replaces=('xfce-utils' 'xfce4-session')
conflicts=('xfce4-session')
provides=('xfce4-session')
install=$pkgname.install
source=("git+http://git.xfce.org/xfce/xfce4-session"
        'xfce-polkit-gnome-authentication-agent-1.desktop'
        '0001-Make-light-locker-command-lock-the-default-lock-comm.patch'
        )
sha256sums=("SKIP"
            '74c94c5f7893d714e04ec7d8b8520c978a5748757a0cdcf5128492f09f31b643'
            '059807c77755d9e8ffd748c8be04afe226b47e2cb650c9c7531973954bf2952f'
            )

pkgver() {
  cd "$srcdir/${_pkgname}"
  git describe --long | sed -r "s/^${_pkgname}-//;s/([^-]*-g)/r\1/;s/-/./g"
}

prepare() {
  cd "$srcdir/${_pkgname}"
  git am ../0001-Make-light-locker-command-lock-the-default-lock-comm.patch  
}

build() {
  cd "$srcdir/${_pkgname}"
  ./autogen.sh \
    --prefix=/usr \
    --sysconfdir=/etc \
    --libexecdir=/usr/lib/xfce4 \
    --localstatedir=/var \
    --disable-static \
    --disable-debug
  make
}

package() {
  cd "$srcdir/${_pkgname}"
  make DESTDIR="$pkgdir" install

  # Provide a default PolicyKit Authentication Agent (FS#42569)
  install -d "$pkgdir/etc/xdg/autostart"
  cp "$srcdir/xfce-polkit-gnome-authentication-agent-1.desktop" \
    "$pkgdir/etc/xdg/autostart/"
}

# vim:set ts=2 sw=2 et:
