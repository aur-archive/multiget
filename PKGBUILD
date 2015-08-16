# Maintainer: sausageandeggs <sausageandeggs@archlinux.us>
# Contributor: Stefan Husmann <stefan-husmann@t-online.de>
# Contributor: Allan McRae <mcrae_allan@hotmail.com>

pkgname=multiget
pkgver=3
pkgrel=2
pkgdesc="Easy to use GUI file downloader - svn version"
url="http://multiget.sourceforge.net"
license=('GPL')
depends=('wxgtk' 'libglade')
makedepends=('intltool' 'svn')
arch=('i686' 'x86_64')
_svntrunk=https://multiget.svn.sourceforge.net/svnroot/multiget
_svnmod=multiget

build() {
cd "$srcdir"

  if [ -d $_svnmod/.svn ]; then
    (cd $_svnmod && svn up -r $pkgver)
  else
    svn co $_svntrunk --config-dir ./ -r $pkgver $_svnmod
  fi
  [ -d "$srcdir/$_svnmod-build" ] && rm -rf "$srcdir/$_svnmod-build"
  cp -r "$srcdir/$_svnmod" "$srcdir/$_svnmod-build"
  cd "$srcdir/$_svnmod-build"

  ./autogen.sh --prefix=/usr --docdir=/usr/share/doc/${_svnmod}
  make
}

package() {
  cd ${srcdir}/$_svnmod-build
  make DESTDIR=${pkgdir} install

  install -Dm644 ${srcdir}/${_svnmod}-build/data/multiget.desktop \
      ${pkgdir}/usr/share/applications/multiget.desktop
  install -Dm644 ${srcdir}/${_svnmod}-build/newicons/48/logo_48.xpm \
      ${pkgdir}/usr/share/pixmaps/multiget.xpm
  # Mv docs to avoid pkg conflict
  mkdir -p ${pkgdir}/usr/share/doc/ #${_svnmod}
  mv $pkgdir/usr/doc/${_svnmod} $pkgdir/usr/share/doc/${_svnmod}
  rmdir $pkgdir/usr/doc
}
