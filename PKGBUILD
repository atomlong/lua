# Maintainer: Juergen Hoetzel <juergen@archlinux.org>
# Contributor: Damir Perisa <damir.perisa@bluewin.ch>

pkgname=lua 
pkgver=5.1.4
pkgrel=5
pkgdesc="A powerful light-weight programming language designed for extending applications." 
arch=('i686' 'x86_64')
url="http://www.lua.org/" 
depends=('readline' 'ncurses') 
license=('MIT')
options=('!makeflags')
source=(http://www.lua.org/ftp/${pkgname}-${pkgver}.tar.gz lua-arch.patch lua-5.1-cflags.diff)
md5sums=('d0870f2de55d59c1c8419f36e8fac150' '6c5953f63904bf20a0183cdab05b80de'\
         '249582bf1fd861ccf492d2c35a9fe732')
sha1sums=('2b11c8e60306efb7f0734b747588f57995493db7' '780a41f93987462a2acd6e338ac648c6b9c01d16'\
         '0d5d6b2aeab1ca8bde5f65d77d40d5a23b79b2c8')

build() { 
  cd "${srcdir}/${pkgname}-${pkgver}"
  patch -p1 -i "${srcdir}/lua-arch.patch"
}

package() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  [ "$CARCH" == "x86_64" ] && patch -Np1 -i ../lua-5.1-cflags.diff
  [ "$CARCH" == "x86_64" ] && export CFLAGS="$CFLAGS -fPIC"
  make INSTALL_DATA="cp -d" TO_LIB="liblua.a liblua.so liblua.so.5.1" LUA_SO=liblua.so  INSTALL_TOP="${pkgdir}/usr" INSTALL_MAN="${pkgdir}/usr/share/man/man1" \
    linux install  || return 1
  install -D -m 644 etc/lua.pc "${pkgdir}/usr/lib/pkgconfig/lua.pc"
  install -D -m644 COPYRIGHT "${pkgdir}/usr/share/licenses/${pkgname}/COPYRIGHT"

  # Install the documentation
  mkdir -p "${pkgdir}/usr/share/doc/lua"
  cp -R doc/* "${pkgdir}/usr/share/doc/lua"
}
