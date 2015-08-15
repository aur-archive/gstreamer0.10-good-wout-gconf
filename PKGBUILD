# $Id: PKGBUILD 135102 2011-08-10 09:44:06Z jgc $
# Baed on: Jan de Groot <jgc@archlinux.org>
# Maintainer: Gustavo Alvarez <sl1pkn07@gmail.com>

pkgname=gstreamer0.10-good-wout-gconf
true && pkgname=('gstreamer0.10-good-wout-gconf' 'gstreamer0.10-good' 'gstreamer0.10-good-plugins')
pkgdesc="GStreamer Multimedia Framework Good plugin libraries WITHOUT GCONF"
pkgver=0.10.30
pkgrel=1
arch=('i686' 'x86_64')
license=('LGPL')
depends=('gstreamer0.10-base>=0.10.34' 'bzip2' 'libxdamage' 'cairo' 'libavc1394' 'libiec61883' 'aalib' 'libshout' 'libdv' 'flac' 'wavpack' 'taglib' 'v4l-utils' 'libcaca' 'bzip2' 'gdk-pixbuf2' 'libpulse' 'jack' 'udev' 'libpng' 'libjpeg')
url="http://gstreamer.freedesktop.org/"
replaces=('gstreamer0.10-aalib' 'gstreamer0.10-wavpack' 'gstreamer0.10-shout2' 'gstreamer0.10-taglib' 'gstreamer0.10-libcaca' 'gstreamer0.10-libpng' 'gstreamer0.10-jpeg' 'gstreamer0.10-cairo' 'gstreamer0.10-flac' 'gstreamer0.10-speex' 'gstreamer0.10-gdkpixbuf' 'gstreamer0.10-dv1394' 'gstreamer0.10-annodex' 'gstreamer0.10-esd' 'gstreamer0.10-cdio' 'gstreamer0.10-dv' 'gstreamer0.10-pulse')
conflicts=('gstreamer0.10-aalib' 'gstreamer0.10-wavpack' 'gstreamer0.10-shout2' 'gstreamer0.10-taglib' 'gstreamer0.10-libcaca' 'gstreamer0.10-libpng' 'gstreamer0.10-jpeg' 'gstreamer0.10-cairo' 'gstreamer0.10-flac' 'gstreamer0.10-speex' 'gstreamer0.10-gdkpixbuf' 'gstreamer0.10-dv1394' 'gstreamer0.10-annodex' 'gstreamer0.10-esd' 'gstreamer0.10-cdio' 'gstreamer0.10-dv' 'gstreamer0.10-pulse' 'gstreamer0.10-bad-plugins<0.10.7')
provides=('gstreamer0.10-good' 'gstreamer0.10-good-plugins')
options=(!libtool !emptydirs)
source=(${url}/src/gst-plugins-good/gst-plugins-good-${pkgver}.tar.bz2)
sha256sums=('b12cba90b27d8423cd0a808939098d19db3996cfb9bf528507c6321782e095f6')

build() {
  cd "${srcdir}/gst-plugins-good-${pkgver}"
  sed -i '/AC_PATH_XTRA/d' configure.ac
  autoreconf
  ./configure --prefix=/usr --sysconfdir=/etc --localstatedir=/var \
    --disable-static --enable-experimental \
    --disable-schemas-install \
    --disable-hal \
    --disable-esd \
    --with-package-name="GStreamer Good Plugins (Archlinux)" \
    --with-package-origin="http://www.archlinux.org/"

  make
  sed -e 's/gst sys ext/gst/' -i Makefile
}
package_gstreamer0.10-good-wout-gconf() {
  cd "${srcdir}/gst-plugins-good-${pkgver}"
}
package_gstreamer0.10-good() {
  cd "${srcdir}/gst-plugins-good-${pkgver}" 
  make GCONF_DISABLE_MAKEFILE_SCHEMA_INSTALL=1 DESTDIR="${pkgdir}" install
  make -C sys DESTDIR="${pkgdir}" install
}
package_gstreamer0.10-good-plugins() {
  cd "${srcdir}/gst-plugins-good-${pkgver}"
  make -C ext GCONF_DISABLE_MAKEFILE_SCHEMA_INSTALL=1 DESTDIR="${pkgdir}" install
  rm -rf "${pkgdir}/etc/gconf"
}
