# Maintainer: Maxime Gauduin <alucryd@archlinux.org>
# Contributor: Bartłomiej Piotrowski <bpiotrowski@archlinux.org>
# Contributor: Ionut Biru <ibiru@archlinux.org>
# Contributor: Tom Newsom <Jeepster@gmx.co.uk>
# Contributor: Paul Mattal <paul@archlinux.org>

pkgname=ffmpeg
pkgver=2.8.4
pkgrel=4
epoch=1
pkgdesc='Complete solution to record, convert and stream audio and video'
arch=('i686' 'x86_64')
url='http://ffmpeg.org/'
license=('GPL3')
depends=('alsa-lib' 'bzip2' 'fontconfig' 'fribidi' 'gnutls' 'gsm' 'lame'
         'libass' 'libbluray' 'libmodplug' 'libpulse' 'libsoxr' 'libssh'
         'libtheora' 'libva' 'libvdpau' 'libwebp' 'opencore-amr' 'openjpeg'
         'opus' 'schroedinger' 'sdl' 'speex' 'v4l-utils' 'xvidcore' 'zlib'
         'libdcadec.so' 'libvidstab.so' 'libvorbis.so' 'libvorbisenc.so'
         'libvpx.so' 'libx264.so' 'libx265.so')
makedepends=('hardening-wrapper' 'ladspa' 'libvdpau' 'yasm')
optdepends=('ladspa: LADSPA filters')
provides=('libavcodec.so' 'libavdevice.so' 'libavfilter.so' 'libavformat.so'
          'libavresample.so' 'libavutil.so' 'libpostproc.so' 'libswresample.so'
          'libswscale.so')
source=(http://ffmpeg.org/releases/ffmpeg-${pkgver}.tar.bz2{,.asc}
        https://github.com/FFmpeg/FFmpeg/commit/7145e80b4f78cff5ed5fee04d4c4d53daaa0e077.patch
        https://github.com/FFmpeg/FFmpeg/commit/6ba42b6482c725a59eb468391544dc0c75b8c6f0.patch
        https://github.com/FFmpeg/FFmpeg/commit/cfda1bea4c18ec1edbc11ecc465f788b02851488.patch)
validpgpkeys=('FCF986EA15E6E293A5644F10B4322F04D67658D8')
sha256sums=('83cc8136a7845546062a43cda9ae3cf0a02f43ef5e434d2f997f055231a75f8e'
            'SKIP'
            '402477e1cdea436bc322016d97f0a48433c7063ab8cb1100490d059b1663e92e'
            'c5e5d2cba239f663004e65f86f87ab608348b5eedb11c0ac6d3403a0b8b49f42'
            'cd285af37d91e04c26a112d6bcbab994e9acf7f49e9f9db06d7c9e8540bb25bd')

prepare() {
  cd ffmpeg-${pkgver}

  # FS#47738
  patch -Np1 -i ../7145e80b4f78cff5ed5fee04d4c4d53daaa0e077.patch
  patch -Np1 -i ../6ba42b6482c725a59eb468391544dc0c75b8c6f0.patch
  patch -Np1 -i ../cfda1bea4c18ec1edbc11ecc465f788b02851488.patch
}

build() {
  cd ffmpeg-${pkgver}

  ./configure \
    --prefix='/usr' \
    --disable-debug \
    --disable-static \
    --disable-stripping \
    --enable-avisynth \
    --enable-avresample \
    --enable-fontconfig \
    --enable-gnutls \
    --enable-gpl \
    --enable-ladspa \
    --enable-libass \
    --enable-libbluray \
    --enable-libdcadec \
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
    --enable-libsoxr \
    --enable-libspeex \
    --enable-libssh \
    --enable-libtheora \
    --enable-libv4l2 \
    --enable-libvidstab \
    --enable-libvorbis \
    --enable-libvpx \
    --enable-libwebp \
    --enable-libx264 \
    --enable-libx265 \
    --enable-libxvid \
    --enable-shared \
    --enable-version3 \
    --enable-x11grab

  make
  make tools/qt-faststart
  make doc/ff{mpeg,play,server}.1
}

package() {
  cd ffmpeg-${pkgver}

  make DESTDIR="${pkgdir}" install install-man
  install -Dm 755 tools/qt-faststart "${pkgdir}"/usr/bin/
}

# vim: ts=2 sw=2 et:
