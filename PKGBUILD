pkgbase=julia
pkgname='julia'
pkgver=1.0.0
pkgrel=2
pkgdesc='High-level, high-performance, dynamic programming language'
arch=('i686' 'x86_64')
url="http://julialang.org"
license=('MIT')
depends=('blas>=3.5.0' 
         'desktop-file-utils' 
         'fftw' 
         'gmp' 
         'gtk-update-icon-cache'
         'hicolor-icon-theme' 
         'lapack>=3.5.0' 
         'libgit2' 
         'libunwind' 
         'libutf8proc>=2'
         'libssh2'
         'mbedtls' 
         'mpfr' 
         'pcre2' 
         'suitesparse' 
         'xdg-utils' )
makedepends=('chrpath' 
             'cmake' 
             'gcc-fortran' 
             'gmp' 
             'gtk-update-icon-cache' 
             'patchelf' 
             'python2' )
options=('!emptydirs' '!strip' '!docs')
provides=('julia')
conflicts=('julia')

source=("https://github.com/JuliaLang/$pkgbase/releases/download/v$pkgver/$pkgbase-$pkgver-full.tar.gz"
        "julia-makefile.patch"
        "julia-libunwind-version.patch"
        "Make.user")
sha256sums=('1a2497977b1d43bb821a5b7475b4054b29938baae8170881c6b8dd4099d133f1'
            '574677d478386fb440b3d6cdd5d0e397fa6997a928bdcace93554fda743d1ed1'
            '4a7532d8d5886aa876a0a281c66add338f0c0f2b9e7b81c65b412da3dc5727f8'
            '47cd164d08bac0b937ceb5ee5934655b06ef50b1459cdb759e698c2a44e6deaa')

prepare() {
  cd $pkgbase

  patch -p1 -i ../julia-libunwind-version.patch
  patch -p0 -i ../julia-makefile.patch # make 'make install' really just install

  cp -v $srcdir/Make.user .
}

build() {
  make $MAKEFLAGS -C $pkgbase prefix=/usr sysconfdir=/etc
}

package() {
  cd $pkgbase
  make $MAKEFLAGS DESTDIR=$pkgdir prefix=/usr sysconfdir=/etc install

  install -Dm644 LICENSE.md "$pkgdir/usr/share/licenses/$pkgbase/LICENSE.md"
}

# vim:set ts=2 sw=2 et:
