# Maintainer: Sébastien Luttringer <seblu@archlinux.org>
# Contributor: Juergen Hoetzel <juergen@archlinux.org>
# Contributor: Damir Perisa <damir.perisa@bluewin.ch>

pkgname=lua
pkgver=5.2.1
pkgrel=2
pkgdesc='A powerful light-weight programming language designed for extending applications'
arch=('i686' 'x86_64')
url='http://www.lua.org/'
depends=('readline')
license=('MIT')
options=('!makeflags' '!emptydirs')
source=("http://www.lua.org/ftp/$pkgname-$pkgver.tar.gz"
        'liblua.so.patch' 'lua.pc')
md5sums=('ae08f641b45d737d12d30291a5e5f6e3'
         'bdc663c7b82ffc0b5df67611621fb625'
         'e7ba6c2b695b0b84a5ea0cbff5fc9067')

build() {
  cd $pkgname-$pkgver
  patch -p1 -i "$srcdir/liblua.so.patch"
  [[ $CARCH == x86_64 ]] && export CFLAGS="$CFLAGS -fPIC"
  make MYCFLAGS="$CFLAGS" MYLDFLAGS="$LDFLAGS" linux
  sed "s/%VER%/${pkgver%.*}/g;s/%REL%/$pkgver/g" ../lua.pc > lua.pc
}

package() {
  cd $pkgname-$pkgver
  make \
    TO_LIB="liblua.a liblua.so liblua.so.5.2 liblua.so.$pkgver" \
    INSTALL_DATA="cp -d" \
    INSTALL_TOP="$pkgdir/usr" \
    INSTALL_MAN="$pkgdir/usr/share/man/man1" \
    install
  install -Dm644 lua.pc "$pkgdir/usr/lib/pkgconfig/lua.pc"
  # Install the documentation
  install -d "$pkgdir/usr/share/doc/lua"
  install -m644 doc/*.{gif,png,css,html} "$pkgdir/usr/share/doc/lua"
}

# vim:set ts=4 sw=4 et:
