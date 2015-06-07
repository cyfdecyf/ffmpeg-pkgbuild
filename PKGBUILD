# Maintainer:  Ionut Biru <ibiru@archlinux.org>
# Maintainer:  Bartłomiej Piotrowski <bpiotrowski@archlinux.org>
# Contributor: Tom Newsom <Jeepster@gmx.co.uk>
# Contributor: Paul Mattal <paul@archlinux.org>

pkgname=ffmpeg
pkgver=2.6.3
pkgrel=3
epoch=1
pkgdesc='Complete and free Internet live audio and video broadcasting solution'
arch=('i686' 'x86_64')
url='http://ffmpeg.org/'
license=('GPL')
depends=(
      'alsa-lib' 'bzip2' 'fontconfig' 'gnutls' 'gsm' 'lame' 'libass' 'libvdpau'
      'libbluray' 'libmodplug' 'libpulse' 'libtheora' 'libva' 'opencore-amr'
      'openjpeg' 'opus' 'schroedinger' 'sdl' 'speex' 'v4l-utils' 'xvidcore'
      'zlib' 'fribidi' 'libssh'
      'libvorbisenc.so' 'libvorbis.so' 'libvpx.so' 'libx264.so' 'libx265.so'
)
makedepends=('libvdpau' 'yasm' 'hardening-wrapper')
source=(http://ffmpeg.org/releases/$pkgname-$pkgver.tar.bz2{,.asc}
        ffmpeg-2.6.3-lavd-xcbgrab-fix-comparison-with-screen-size.patch)
validpgpkeys=('FCF986EA15E6E293A5644F10B4322F04D67658D8') # ffmpeg-devel
md5sums=('e2cc3c209f91393d35ab58598e41cf22'
         'SKIP'
         'ac9f115dced48b66e36249349a29347e')

prepare() {
  cd $pkgname-$pkgver
  patch -p1 -i ../ffmpeg-2.6.3-lavd-xcbgrab-fix-comparison-with-screen-size.patch
}

build() {
  cd $pkgname-$pkgver

  ./configure \
    --prefix=/usr \
    --disable-debug \
    --disable-static \
    --disable-stripping \
    --enable-avisynth \
    --enable-avresample \
    --enable-fontconfig \
    --enable-gnutls \
    --enable-gpl \
    --enable-libass \
    --enable-libbluray \
    --enable-libfreetype \
    --enable-libfribidi \
    --enable-libgsm \
    --enable-libmodplug \
    --enable-libmp3lame \
    --enable-libopencore_amrnb \
    --enable-libopencore_amrwb \
    --enable-libopenjpeg \
    --enable-libopus \
    --enable-libpulse \
    --enable-libschroedinger \
    --enable-libspeex \
    --enable-libssh \
    --enable-libtheora \
    --enable-libv4l2 \
    --enable-libvorbis \
    --enable-libvpx \
    --enable-libx264 \
    --enable-libx265 \
    --enable-libxvid \
    --enable-shared \
    --enable-version3 \
    --enable-x11grab \

  make
  make tools/qt-faststart
  make doc/ff{mpeg,play,server}.1
}

package() {
  cd $pkgname-$pkgver
  make DESTDIR="$pkgdir" install install-man
  install -Dm755 tools/qt-faststart "$pkgdir"/usr/bin/qt-faststart
}
