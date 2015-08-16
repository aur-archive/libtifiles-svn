# Contributor: Jon Sturm <Jasturm002@aol.com>
_pkgname=libtifiles
pkgname=$_pkgname-svn
pkgver=4340
pkgrel=1
pkgdesc="TI File format library"
arch=(i686 x86_64)
url="http://tilp.info/"
license=('GPL')
depends=('zlib' 'glib2' 'libticonv' )
makedepends=('subversion')
provides=('libtifiles' 'libtifiles2')
conflicts=('libtifiles' 'libtifiles2')
options=('force' '!libtool')
#md5sums=() #generate with 'makepkg -g'

_svnmod=$_pkgname
_svntrunk=http://svn.tilp.info/repos/tilp/$_svnmod/trunk

build() {
  cd "$srcdir"

  if [ -d $_svnmod/.svn ]; then
    (cd $_svnmod && svn up -r $pkgver)
  else
    svn co $_svntrunk --config-dir ./ -r $pkgver $_svnmod
  fi

  msg "SVN checkout done or server timeout"
  msg "Starting make..."

  rm -rf "$srcdir/$_svnmod-build"
  cp -r "$srcdir/$_svnmod" "$srcdir/$_svnmod-build"
  cd "$srcdir/$_svnmod-build"

  #
  # BUILD
  #
  autoreconf -i -f
  ./configure --prefix=/usr
  make || return 1
  make DESTDIR="$pkgdir/" install
}
