# Maintainer: Sébastien Luttringer <seblu@archlinux.org>
# Contributor: Juergen Hoetzel <juergen@archlinux.org>
# Contributor: Damir Perisa <damir.perisa@bluewin.ch>

pkgname=lua
pkgver=5.2.4
pkgrel=1
pkgdesc='Powerful light-weight programming language designed for extending applications'
arch=('i686' 'x86_64')
url='http://www.lua.org/'
depends=('readline')
license=('MIT')
options=('!makeflags' '!emptydirs')
source=(http://www.lua.org/ftp/$pkgname-$pkgver.tar.gz
        liblua.so.patch
        lua.pc
        LICENSE)
md5sums=('913fdb32207046b273fdb17aad70be13'
         'bdc663c7b82ffc0b5df67611621fb625'
         'e7ba6c2b695b0b84a5ea0cbff5fc9067'
         '0e2bd67b909b9ff673da844ca3480df2')

prepare() {
  cd $pkgname-$pkgver
  patch -p1 -i ../liblua.so.patch
}

build() {
  cd $pkgname-$pkgver

  export CFLAGS="$CFLAGS -fPIC"
  make MYCFLAGS="$CFLAGS" MYLDFLAGS="$LDFLAGS" linux

  sed "s/%VER%/${pkgver%.*}/g;s/%REL%/$pkgver/g" ../lua.pc > lua.pc
}

package() {
  cd $pkgname-$pkgver

  make \
    TO_LIB='liblua.a liblua.so liblua.so.5.2 liblua.so.5.2.4' \
    INSTALL_DATA='cp -d' \
    INSTALL_TOP="$pkgdir"/usr \
    INSTALL_MAN="$pkgdir"/usr/share/man/man1 \
    install
  install -Dm644 lua.pc "$pkgdir"/usr/lib/pkgconfig/lua.pc

  # Install the documentation
  install -d "$pkgdir"/usr/share/doc/lua
  install -m644 doc/*.{gif,png,css,html} "$pkgdir"/usr/share/doc/lua
  install -Dm644 ../LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
}
