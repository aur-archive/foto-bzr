# Maintainer: Ner0

pkgname=foto-bzr
pkgver=117
pkgrel=1
pkgdesc="A very simple image viewer and album manager written in Vala using Gtk3, Clutter, Cairo and Granite."
arch=('i686' 'x86_64')
url="https://launchpad.net/foto"
license=('GPL3')
depends=('glib2' 'granite-bzr' 'clutter' 'clutter-gtk' 'gtk3' 'libgee' 'sqlite' 'libgexiv2_05' 'desktop-file-utils')
makedepends=('bzr' 'vala' 'cmake')
install=foto.install

_bzrtrunk=lp:foto
_bzrmod=foto

build() {
  msg "Connecting to Bazaar server...."

  if [[ -d "$_bzrmod" ]]; then
    cd "$_bzrmod" && bzr pull "$_bzrtrunk" -r $pkgver && cd ..
    msg "The local files are updated."
  else
    bzr branch "$_bzrtrunk" "$_bzrmod" -r $pkgver
  fi

  msg "BZR checkout done or server timeout"
  msg "Starting make..."

  rm -rf "$_bzrmod-build"
  cp -rf "$_bzrmod" "$_bzrmod-build"
  cd "$_bzrmod-build"

  rm -rf build/
  mkdir build
  cd build

  cmake .. -DCMAKE_INSTALL_PREFIX=/usr -DGSETTINGS_COMPILE=OFF -DGSETTINGS_LOCALINSTALL=OFF -DICON_UPDATE=OFF
  make
}

package() {
  cd "$_bzrmod-build/build"
  make GCONF_DISABLE_MAKEFILE_SCHEMA_INSTALL=1 DESTDIR="$pkgdir/" install
}
