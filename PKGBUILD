# Maintainer: Vorzard <vorzard at plexomat dot com>

pkgname=tcl86
pkgver=8.6.0
pkgrel=1
provides=('tcl=8.6')
replaces=('sqlite-tcl')
conflicts=('tcl' 'sqlite-tcl')
pkgdesc="The Tcl scripting language"
url="http://tcl.tk/"
arch=('i686' 'x86_64')
license=('custom')
source=("http://downloads.sourceforge.net/sourceforge/tcl/tcl$pkgver-src.tar.gz")
sha1sums=('fc57fc08ab113740a702bb67d4f350f8ec85ef58')

build() {
  cd $srcdir/tcl$pkgver/unix
  if [ "$CARCH" = "x86_64" ]; then
    ./configure --prefix=/usr --mandir=/usr/share/man --enable-64bit
  else
    ./configure --prefix=/usr --mandir=/usr/share/man --disable-64bit
  fi
  make
}

package() {
  cd $srcdir/tcl$pkgver/unix
  make DESTDIR="$pkgdir" install install-private-headers
  ln -sf tclsh8.6 $pkgdir/usr/bin/tclsh
  install -Dm644 $srcdir/tcl$pkgver/license.terms $pkgdir/usr/share/licenses/tcl/LICENSE

  # Remove buildroot traces

  sed -i \
    -e "s,^TCL_BUILD_LIB_SPEC='-L.*/unix,TCL_BUILD_LIB_SPEC='-L/usr/lib," \
    -e "s,^TCL_SRC_DIR='.*',TCL_SRC_DIR='/usr/include'," \
    -e "s,^TCL_BUILD_STUB_LIB_SPEC='-L.*/unix,TCL_BUILD_STUB_LIB_SPEC='-L/usr/lib," \
    -e "s,^TCL_BUILD_STUB_LIB_PATH='.*/unix,TCL_BUILD_STUB_LIB_PATH='/usr/lib," \
    $pkgdir/usr/lib/tclConfig.sh

  sed -i \
    -e "s,^ITCL_BUILD_LIB_SPEC='-L.*/pkgs,ITCL_BUILD_LIB_SPEC='-L/usr/lib," \
    -e "s,^itcl_BUILD_LIB_SPEC='-L.*/pkgs,itcl_BUILD_LIB_SPEC='-L/usr/lib," \
    -e "s,^ITCL_BUILD_STUB_LIB_SPEC='-L.*/pkgs,ITCL_BUILD_STUB_LIB_SPEC='-L/usr/lib," \
    -e "s,^itcl_BUILD_STUB_LIB_SPEC='-L.*/pkgs,itcl_BUILD_STUB_LIB_SPEC='-L/usr/lib," \
    -e "s,^ITCL_BUILD_STUB_LIB_PATH='.*/pkgs,ITCL_BUILD_STUB_LIB_PATH='/usr/lib," \
    -e "s,^itcl_BUILD_STUB_LIB_PATH='.*/pkgs,itcl_BUILD_STUB_LIB_PATH='/usr/lib," \
    -e "s,^ITCL_SRC_DIR='.*',ITCL_SRC_DIR='/usr/include'," \
    -e "s,^itcl_SRC_DIR='.*',itcl_SRC_DIR='/usr/include'," \
    -e "s,^ITCL_INCLUDE_SPEC='.*',ITCL_INCLUDE_SPEC='-I/usr/include'," \
    -e "s,^itcl_INCLUDE_SPEC='.*',itcl_INCLUDE_SPEC='-I/usr/include'," \
    $pkgdir/usr/lib/itcl4.0.0/itclConfig.sh

  sed -i \
    -e "s,^tdbc_BUILD_STUB_LIB_SPEC=\"-L.*/pkgs,tdbc_BUILD_STUB_LIB_SPEC=\"-L/usr/lib," \
    -e "s,^TDBC_BUILD_STUB_LIB_SPEC=\"-L.*/pkgs,TDBC_BUILD_STUB_LIB_SPEC=\"-L/usr/lib," \
    -e "s,^tdbc_BUILD_STUB_LIB_PATH=\".*/pkgs,tdbc_BUILD_STUB_LIB_PATH=\"/usr/lib," \
    -e "s,^TDBC_BUILD_STUB_LIB_PATH=\".*/pkgs,TDBC_BUILD_STUB_LIB_PATH=\"/usr/lib," \
    -e "s,^tdbc_SRC_DIR=\".*\",tdbc_SRC_DIR=\"/usr/include\"," \
    -e "s,^TDBC_SRC_DIR=\".*\",TDBC_SRC_DIR=\"/usr/include\"," \
    -e "s,^tdbc_BUILD_INCLUDE_SPEC=\".*\",tdbc_BUILD_INCLUDE_SPEC=\"-I/usr/include\"," \
    -e "s,^TDBC_BUILD_INCLUDE_SPEC=\".*\",TDBC_BUILD_INCLUDE_SPEC=\"-I/usr/include\"," \
    -e "s,^tdbc_BUILD_LIBRARY_PATH=\".*/pkgs,tdbc_BUILD_LIBRARY_PATH=\"/usr/lib," \
    -e "s,^TDBC_BUILD_LIBRARY_PATH=\".*/pkgs,TDBC_BUILD_LIBRARY_PATH=\"/usr/lib," \
    $pkgdir/usr/lib/tdbc1.0.0/tdbcConfig.sh
}
