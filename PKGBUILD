# Maintainer : Ionut Biru <ibiru@archlinux.org>
# Contributor: Tom Newsom <Jeepster@gmx.co.uk>
# Contributor: Paul Mattal <paul@archlinux.org>

pkgname=ffmpeg
pkgver=25679
pkgrel=1
pkgdesc="Complete and free Internet live audio and video broadcasting solution for Linux/Unix"
arch=('i686' 'x86_64')
url="http://ffmpeg.org/"
license=('GPL')
depends=('bzip2' 'lame' 'sdl' 'libvorbis' 'faac' 'xvidcore' 'zlib' 'x264' 'libtheora' 'opencore-amr' 'alsa-lib' 'libvdpau' 'libxfixes' 'schroedinger' 'libvpx' 'libva>=1.0.4' 'openjpeg')
makedepends=('yasm')
#remake snapshot with: svn export svn://svn.ffmpeg.org/ffmpeg/trunk/@25472
source=(ftp://ftp.archlinux.org/other/ffmpeg/ffmpeg-${pkgver}.tar.xz)
options=('force')
#source=(http://ffmpeg.org/releases//releases/ffmpeg-${pkgver}.tar.bz2)
md5sums=('9fdc03624ffd744fb25964e2f8dcd09d')

build() {
  cd "$srcdir/$pkgname"

  ./configure \
    --prefix=/usr \
    --enable-gpl \
    --enable-libmp3lame \
    --enable-libvorbis \
    --enable-libfaac \
    --enable-libxvid \
    --enable-libx264 \
    --enable-libvpx \
    --enable-libtheora \
    --enable-postproc \
    --enable-shared \
    --enable-pthreads \
    --enable-x11grab \
    --enable-libopencore_amrnb \
    --enable-libopencore_amrwb \
    --enable-libschroedinger \
    --enable-libopenjpeg \
    --enable-version3 \
    --enable-nonfree \
    --enable-runtime-cpudetect \
    --disable-debug  # libfaac is nonfree

  make
  make tools/qt-faststart
  make doc/ff{mpeg,play,server}.1

  make DESTDIR="$pkgdir" install install-man
  install -D -m755 tools/qt-faststart "$pkgdir/usr/bin/qt-faststart"
}

# vim:set ts=2 sw=2 et:
