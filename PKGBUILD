# Maintainer: Sébastien Luttringer <seblu@archlinux.org>
# Contributor: Juergen Hoetzel <juergen@archlinux.org>
# Contributor: Damir Perisa <damir.perisa@bluewin.ch>

pkgname=lua
pkgver=5.3.0
pkgrel=1
pkgdesc='Powerful lightweight programming language designed for extending applications'
arch=('i686' 'x86_64')
url='http://www.lua.org/'
depends=('readline')
license=('MIT')
options=('!emptydirs')
source=(http://www.lua.org/ftp/lua-$pkgver.tar.gz
        liblua.so.patch
        lua.pc
        LICENSE)
md5sums=('a1b0a7e92d0c85bbff7a8d27bf29f8af'
         '85fe4e5f780376457eba3bc23d2cb2d3'
         'e7ba6c2b695b0b84a5ea0cbff5fc9067'
         '0e2bd67b909b9ff673da844ca3480df2')

prepare() {
  cd lua-$pkgver
  patch -p1 -i ../liblua.so.patch

  sed "s/%VER%/${pkgver%.*}/g;s/%REL%/$pkgver/g" ../lua.pc > lua.pc
}

build() {
  cd lua-$pkgver

  make MYCFLAGS="$CFLAGS -fPIC" MYLDFLAGS="$LDFLAGS" linux
}

package() {
  cd lua-$pkgver

  make \
    TO_LIB="liblua.a liblua.so liblua.so.5.3 liblua.so.$pkgver" \
    INSTALL_DATA='cp -d' \
    INSTALL_TOP="$pkgdir"/usr \
    INSTALL_MAN="$pkgdir"/usr/share/man/man1 \
    install
  install -Dm644 lua.pc "$pkgdir"/usr/lib/pkgconfig/$pkgname.pc

  install -d "$pkgdir"/usr/share/doc/$pkgname
  install -m644 doc/*.{gif,png,css,html} "$pkgdir"/usr/share/doc/$pkgname
  install -Dm644 ../LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
}
