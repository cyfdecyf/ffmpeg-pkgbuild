# Maintainer : Ionut Biru <ibiru@archlinux.org>
# Contributor: Tom Newsom <Jeepster@gmx.co.uk>
# Contributor: Paul Mattal <paul@archlinux.org>

pkgname=ffmpeg
pkgver=20110330
pkgrel=2
pkgdesc="Complete and free Internet live audio and video broadcasting solution for Linux/Unix"
arch=('i686' 'x86_64')
url="http://ffmpeg.org/"
license=('GPL')
depends=('bzip2' 'lame' 'sdl' 'libvorbis' 'xvidcore' 'zlib' 'x264' 'libtheora' 'opencore-amr' 'alsa-lib' 'libvdpau' 'libxfixes' 'schroedinger' 'libvpx' 'libva' 'openjpeg')
makedepends=('yasm' 'git')
#git clone git://git.videolan.org/ffmpeg.git
source=(ftp://ftp.archlinux.org/other/ffmpeg/${pkgname}-${pkgver}.tar.xz
        avutils-make-aes-and-sha-public.patch)
md5sums=('dd682a876a496b9f9ae8afb3b3b70389'
         '06eb45335669cb742fdcbea48f0605ce')

build() {
  cd "$srcdir/$pkgname"

  patch -Np1 -i "$srcdir/avutils-make-aes-and-sha-public.patch"

  ./configure \
    --prefix=/usr \
    --enable-libmp3lame \
    --enable-libvorbis \
    --enable-libxvid \
    --enable-libx264 \
    --enable-libvpx \
    --enable-libtheora \
    --enable-postproc \
    --enable-shared \
    --enable-x11grab \
    --enable-libopencore_amrnb \
    --enable-libopencore_amrwb \
    --enable-libschroedinger \
    --enable-libopenjpeg \
    --enable-gpl \
    --enable-version3 \
    --enable-runtime-cpudetect \
    --disable-debug

  make
  make tools/qt-faststart
  make doc/ff{mpeg,play,server}.1

  make DESTDIR="$pkgdir" install install-man
  install -D -m755 tools/qt-faststart "$pkgdir/usr/bin/qt-faststart"
}

# vim:set ts=2 sw=2 et:
