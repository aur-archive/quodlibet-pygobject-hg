# Maintainer: Pedro Martinez-Julia <pedromj@um.es>
# Contributor: Anton Shestakov <engored*ya.ru>

pkgname=quodlibet-pygobject-hg
pkgver=5623
pkgrel=1
pkgdesc='Audio library tagger, manager, and player for GTK+. PyGObject version (from Mercurial).'
arch=(any)
url='http://code.google.com/p/quodlibet/'
license=('GPL2')
depends=('gstreamer' 'gst-plugins-base' 'gst-plugins-base-libs'
         'gst-plugins-good' 'gst-plugins-ugly' 
         'mutagen' 'python2-gobject' 'python2')
makedepends=('mercurial' 'intltool')
optdepends=('dbus-python: audio devices support.'
            'python-gpod: iPod support.'
            'python-feedparser: audio feeds (podcasts) support.')
conflicts=('quodlibet' 'quodlibet-svn' 'quodlibet-no-exfalso')
provides=('quodlibet')
source=('icon-cache.patch')
sha1sums=('a137985a74a1f5efda08db4bda05a1196b2e6a01')
install=quodlibet.install

_hgroot='https://quodlibet.googlecode.com/hg'
_hgrepo='quodlibet'
_hgbranch='pygobject-port'

build() {
  if [ ! -d "$_hgrepo" ] ; then
    hg clone -b "$_hgbranch" "$_hgroot" "$_hgrepo"
  fi
  cd "$_hgrepo"
  hg update "$_hgbranch"
  
  cd "$srcdir"
  
  msg 'Making a local copy of the HG repository...'
  rm -rf "$_hgrepo-build"
  hg clone "$_hgrepo" "$_hgrepo-build"
  cd "$_hgrepo-build"
  hg update "$_hgbranch"

  msg 'Applying patches...'
  patch -Np1 -i ../icon-cache.patch
  cd "quodlibet"

  sed -i -e 's/env python/env python2/' *.py

  ./setup.py build
}  

package() {
  cd "$_hgrepo-build/quodlibet"
  ./setup.py install --prefix="$pkgdir/usr"
}
