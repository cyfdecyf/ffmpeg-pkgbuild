# Maintainer : Ionut Biru <ibiru@archlinux.org>
# Contributor: Tom Newsom <Jeepster@gmx.co.uk>
# Contributor: Paul Mattal <paul@archlinux.org>

pkgname=ffmpeg
pkgver=1.1.3
pkgrel=1
epoch=1
pkgdesc="Complete and free Internet live audio and video broadcasting solution for Linux/Unix"
arch=('i686' 'x86_64')
url="http://ffmpeg.org/"
license=('GPL')
depends=(
      'alsa-lib' 'bzip2' 'fontconfig' 'gsm' 'lame' 'libass'
      'libbluray' 'libmodplug' 'libpulse' 'libtheora' 'libva' 'libvorbis' 'libvpx'
      'opencore-amr' 'openjpeg' 'opus' 'rtmpdump' 'schroedinger' 'sdl' 'speex'
      'v4l-utils' 'x264' 'xvidcore' 'zlib'
      )
makedepends=('libvdpau' 'yasm')
source=(http://ffmpeg.org/releases/$pkgname-$pkgver.tar.bz2)
sha256sums=('a70057eba6256fab7342f863e7bb556d14cbed207b5b5b884a0879d3f16ca0a8')

build() {
  cd $pkgname-$pkgver

  ./configure \
    --prefix=/usr \
    --disable-debug \
    --disable-static \
    --enable-avresample \
    --enable-fontconfig \
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
    --enable-postproc \
    --enable-runtime-cpudetect \
    --enable-shared \
    --enable-version3 \
    --enable-x11grab
 

  make
  make tools/qt-faststart
  make doc/ff{mpeg,play,server}.1
}

package() {
  cd $pkgname-$pkgver
  make DESTDIR="$pkgdir" install install-man
  install -D -m755 tools/qt-faststart "$pkgdir/usr/bin/qt-faststart"
}

# vim:set ts=2 sw=2 et:
