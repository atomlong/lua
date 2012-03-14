# Maintainer: Juergen Hoetzel <juergen@archlinux.org>
# Contributor: Damir Perisa <damir.perisa@bluewin.ch>

pkgname=lua 
pkgver=5.1.5
pkgrel=1
pkgdesc="A powerful light-weight programming language designed for extending applications" 
arch=('i686' 'x86_64')
url="http://www.lua.org/"
depends=('readline')
license=('MIT')
options=('!makeflags' '!emptydirs')
source=(http://www.lua.org/ftp/${pkgname}-${pkgver}.tar.gz
        lua-arch.patch lua-5.1-cflags.diff)
md5sums=('2e115fe26e435e33b0d5c022e4490567'
         '6c5953f63904bf20a0183cdab05b80de'
         '249582bf1fd861ccf492d2c35a9fe732')

build() { 
  cd "${srcdir}/${pkgname}-${pkgver}"
  patch -p1 -i "${srcdir}/lua-arch.patch"
  patch -p1 -i "${srcdir}/lua-5.1-cflags.diff"
  export CFLAGS="$CFLAGS -fPIC"

  make INSTALL_DATA="cp -d" TO_LIB="liblua.a liblua.so liblua.so.5.1" LUA_SO=liblua.so \
    INSTALL_TOP="${pkgdir}/usr" INSTALL_MAN="${pkgdir}/usr/share/man/man1" \
    linux
}

package() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  make INSTALL_DATA="cp -d" TO_LIB="liblua.a liblua.so liblua.so.5.1" LUA_SO=liblua.so \
    INSTALL_TOP="${pkgdir}/usr" INSTALL_MAN="${pkgdir}/usr/share/man/man1" \
    install
  install -D -m644 etc/lua.pc "${pkgdir}/usr/lib/pkgconfig/lua.pc"
  install -D -m644 COPYRIGHT "${pkgdir}/usr/share/licenses/${pkgname}/COPYRIGHT"

  # Install the documentation
  install -d "${pkgdir}/usr/share/doc/lua"
  install -m644 doc/*.{gif,png,css,html} "${pkgdir}/usr/share/doc/lua"
}
