# Maintainer:  Ionut Biru <ibiru@archlinux.org>
# Maintainer:  Bartłomiej Piotrowski <nospam@bpiotrowski.pl>
# Contributor: Tom Newsom <Jeepster@gmx.co.uk>
# Contributor: Paul Mattal <paul@archlinux.org>

pkgname=ffmpeg
pkgver=2.1.1
pkgrel=3
epoch=1
pkgdesc='Complete and free Internet live audio and video broadcasting solution'
arch=('i686' 'x86_64')
url='http://ffmpeg.org/'
license=('GPL')
depends=(
      'alsa-lib' 'bzip2' 'fontconfig' 'gnutls' 'gsm' 'lame' 'libass'
      'libbluray' 'libmodplug' 'libpulse' 'libtheora' 'libva' 'libvorbis' 'libvpx'
      'opencore-amr' 'openjpeg' 'opus' 'rtmpdump' 'schroedinger' 'sdl' 'speex'
      'v4l-utils' 'x264' 'xvidcore' 'zlib'
      )
makedepends=('libvdpau' 'yasm')
source=(http://ffmpeg.org/releases/$pkgname-$pkgver.tar.bz2
        ffmpeg-2.1.1-freetype2.patch)
md5sums=('2719ab2b3311ac3775b9cdeb66c54849'
         '4b5dd079a40f44f4e0d00cdbc9d52ec3')

prepare() {
  cd $pkgname-$pkgver
  patch -p1 -i ../ffmpeg-2.1.1-freetype2.patch
}

build() {
  cd $pkgname-$pkgver

  ./configure \
    --prefix=/usr \
    --disable-debug \
    --disable-static \
    --enable-avresample \
    --enable-dxva2 \
    --enable-fontconfig \
    --enable-gnutls \
    --enable-gpl \
    --enable-libass \
    --enable-libbluray \
    --enable-libfreetype \
    --enable-libgsm \
    --enable-libmodplug \
    --enable-libmp3lame \
    --enable-libopencore_amrnb \
    --enable-libopencore_amrwb \
    --enable-libopenjpeg \
    --enable-libopus \
    --enable-libpulse \
    --enable-librtmp \
    --enable-libschroedinger \
    --enable-libspeex \
    --enable-libtheora \
    --enable-libv4l2 \
    --enable-libvorbis \
    --enable-libvpx \
    --enable-libx264 \
    --enable-libxvid \
    --enable-pic \
    --enable-postproc \
    --enable-runtime-cpudetect \
    --enable-shared \
    --enable-swresample \
    --enable-vdpau \
    --enable-version3 \
    --enable-x11grab

  make
  make tools/qt-faststart
  make doc/ff{mpeg,play,server}.1
}

package() {
  cd $pkgname-$pkgver
  make DESTDIR="$pkgdir" install install-man
  install -Dm755 tools/qt-faststart "$pkgdir"/usr/bin/qt-faststart
}

# vim:set ts=2 sw=2 et:
