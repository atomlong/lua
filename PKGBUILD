# Maintainer: Juergen Hoetzel <juergen@archlinux.org>
# Contributor: Damir Perisa <damir.perisa@bluewin.ch>
#

pkgname=lua 
pkgver=5.1.3
pkgrel=3
pkgdesc="A powerful light-weight programming language designed for extending applications." 
arch=(i686 x86_64)
url="http://www.lua.org/" 
depends=(readline) 
license=(MIT)
options=('!makeflags')
source=($url/ftp/$pkgname-$pkgver.tar.gz $pkgname-arch.patch 'lua-5.1-cflags.diff' \
	lua-${pkgver}-official-patch1.diff\
	lua-${pkgver}-official-patch2.diff\
	lua-${pkgver}-official-patch3.diff\
	lua-${pkgver}-official-patch4.diff)
md5sums=('a70a8dfaa150e047866dc01a46272599' '1bd1164a19abf9165e231ba0d8a0bbc7'\
         '249582bf1fd861ccf492d2c35a9fe732' '203027f2ddcfaf5697293c23d7915f57'\
         'd06c5b23daaa414348948d5b8c308d6f' 'dde56cd1d48a8bb2fb661a9aaf8380ad'\
         '616808cee32ff328077b848131df7670')

build() { 
  cd $startdir/src/$pkgname-$pkgver 
  patch -p1 -i $startdir/src/$pkgname-arch.patch || return 1
  patch --ignore-whitespace src/luaconf.h $startdir/src/lua-${pkgver}-official-patch1.diff || return 1
  patch -p0  -i $startdir/src/lua-${pkgver}-official-patch2.diff || return 1
  patch -p0  -i $startdir/src/lua-${pkgver}-official-patch3.diff || return 1
  patch -p0  -i $startdir/src/lua-${pkgver}-official-patch4.diff || return 1
  [ "$CARCH" == "x86_64" ] && patch -Np1 -i ../lua-5.1-cflags.diff
  [ "$CARCH" == "x86_64" ] && export CFLAGS="$CFLAGS -fPIC"
  make INSTALL_DATA="cp -d" TO_LIB="liblua.a liblua.so.5.1 liblua.so" LUA_SO=liblua.so  INSTALL_TOP=$startdir/pkg/usr INSTALL_MAN=$startdir/pkg/usr/share/man/man1 \
    linux install  || return 1
  install -D -m 644 etc/lua.pc $startdir/pkg/usr/lib/pkgconfig/lua.pc
  install -D -m644 COPYRIGHT $startdir/pkg/usr/share/licenses/$pkgname/COPYRIGHT
}
# vim: ts=2 sw=2 et ft=sh
