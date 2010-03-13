# Maintainer : Ionut Biru <ibiru@archlinux.org>
# Contributor: Tom Newsom <Jeepster@gmx.co.uk>
# Contributor: Paul Mattal <paul@archlinux.org>

pkgname=ffmpeg
pkgver=22511
pkgrel=1
pkgdesc="Complete and free Internet live audio and video broadcasting solution for Linux/Unix"
arch=('i686' 'x86_64')
url="http://ffmpeg.org/"
license=('GPL')
depends=('lame' 'sdl' 'libvorbis' 'faad2>=2.7' 'faac' 'xvidcore' 'zlib' 'imlib2' 'x264>=20100312' 'libtheora' 'opencore-amr>=0.1.2' 'alsa-lib' 'libvdpau' 'libxfixes')
makedepends=('yasm')
options=('force')
#remake snapshot with: svn export svn://svn.ffmpeg.org/ffmpeg/trunk/@21104
source=(ftp://ftp.archlinux.org/other/ffmpeg/ffmpeg-${pkgver}.tar.bz2)
#source=(http://ffmpeg.org/releases//releases/ffmpeg-${pkgver}.tar.bz2)
sha256sums=('da9f5a89f41b1358b1d07a4dc77fba14c686ac3d9765fdc865d8e7c211782267')

build() {
  cd "$srcdir/$pkgname" || return 1
  export CFLAGS="$CFLAGS -fno-strict-aliasing"

  ./configure \
  --prefix=/usr \
  --enable-gpl \
  --enable-libmp3lame \
  --enable-libvorbis \
  --enable-libfaac \
  --enable-libfaad \
  --enable-libxvid \
  --enable-libx264 \
  --enable-libtheora \
  --enable-postproc \
  --enable-shared \
  --enable-pthreads \
  --enable-x11grab \
  --enable-libopencore_amrnb \
  --enable-libopencore_amrwb \
  --enable-version3 \
  --enable-nonfree \
  --enable-runtime-cpudetect || return 1 # libfaac is nonfree

  make || return 1
  make tools/qt-faststart || return 1
  make doc/ff{mpeg,play,server}.1 || return 1

  make DESTDIR="$pkgdir" install install-man || return 1
  install -D -m755 tools/qt-faststart "$pkgdir/usr/bin/qt-faststart" || return 1

  # since makepkg currently declines to strip .a files, do this for now
  strip --strip-debug "$pkgdir"/usr/lib/*.a || return 1
}

# vim:set ts=2 sw=2 et:
