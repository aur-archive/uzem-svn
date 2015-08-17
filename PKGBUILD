# Maintainer: Louis-Guillaume Gagnon <luidge6@gmail.com>
pkgname=uzem-svn  
pkgver=211
pkgrel=2
pkgdesc="A Uzebox 8-bit game console emulator"
url="http://belogic.com/uzebox"
arch=('i686' 'x86_64')
license=('GPL3')
depends=('sdl')
makedepends=('subversion' 'gcc')

_svntrunk="http://uzebox.googlecode.com/svn/trunk/tools/uzem"
_svnmod="uzem"

build() {

  cd "$srcdir"
  msg "Connecting to SVN server...."

  if [[ -d "$_svnmod/.svn" ]]; then
    (cd "$_svnmod" && svn up -r "$pkgver")
  else
    svn co "$_svntrunk" --config-dir ./ -r "$pkgver" "$_svnmod"
  fi

  msg "SVN checkout done or server timeout"
  msg "Starting build..."

  rm -rf "$srcdir/$_svnmod-build"
  svn export "$srcdir/$_svnmod" "$srcdir/$_svnmod-build"
  cd "$srcdir/$_svnmod-build"

  make 
}

package() {
  mkdir -p "$pkgdir/usr/bin"
  cp "$srcdir/$_svnmod-build/uzem" "$pkgdir/usr/bin/uzem"
  cp "$srcdir/$_svnmod-build/uzemdbg" "$pkgdir/usr/bin/uzemdbg"
}
