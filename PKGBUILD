# Maintainer: Maxime Gauduin <alucryd@archlinux.org>
# Contributor: Bartłomiej Piotrowski <bpiotrowski@archlinux.org>
# Contributor: Ionut Biru <ibiru@archlinux.org>
# Contributor: Tom Newsom <Jeepster@gmx.co.uk>
# Contributor: Paul Mattal <paul@archlinux.org>

pkgname=ffmpeg
pkgver=6.0
pkgrel=8
epoch=2
pkgdesc='Complete solution to record, convert and stream audio and video'
arch=(x86_64)
url=https://ffmpeg.org/
license=(GPL3)
depends=(
  alsa-lib
  aom
  bzip2
  fontconfig
  fribidi
  gmp
  gnutls
  gsm
  jack
  lame
  libass.so
  libavc1394
  libbluray.so
  libbs2b.so
  libdav1d.so
  libdrm
  libfdk-aac
  libfreetype.so
  libgl
  libiec61883
  libjxl.so
  libmfx
  libmodplug
  libopenmpt.so
  libpulse
  librav1e.so
  libraw1394
  librsvg-2.so
  libsoxr
  libssh
  libtheora
  libva.so
  libva-drm.so
  libva-x11.so
  libvdpau
  libvidstab.so
  libvorbisenc.so
  libvorbis.so
  libvpx.so
  libwebp
  libx11
  libx264.so
  libx265.so
  libxcb
  libxext
  libxml2
  libxv
  libxvidcore.so
  libzimg.so
  ocl-icd
  opencore-amr
  openjpeg2
  onevpl
  opus
  sdl2
  speex
  srt
  svt-av1
  v4l-utils
  vmaf
  vulkan-icd-loader
  xz
  zlib
)
makedepends=(
  amf-headers
  avisynthplus
  git
  ladspa
  mesa
  nasm
  opencl-headers
  vulkan-headers
)
optdepends=(
  'avisynthplus: AviSynthPlus support'
  'intel-media-sdk: Intel QuickSync support'
  'ladspa: LADSPA filters'
  'nvidia-utils: Nvidia NVDEC/NVENC support'
  'onevpl-intel-gpu: oneVPL runtime implementation for Intel GPUs (Tiger Lake and newer)'
)
provides=(
  libavcodec.so
  libavdevice.so
  libavfilter.so
  libavformat.so
  libavutil.so
  libpostproc.so
  libswresample.so
  libswscale.so
)
options=(
  debug
)
_tag=3949db4d261748a9f34358a388ee255ad1a7f0c0
source=(
  git+https://git.ffmpeg.org/ffmpeg.git?signed#tag=${_tag}
  add-av_stream_get_first_dts-for-chromium.patch
  mathops-asm-fix.patch
)
b2sums=('SKIP'
        '555274228e09a233d92beb365d413ff5c718a782008075552cafb2130a3783cf976b51dfe4513c15777fb6e8397a34122d475080f2c4483e8feea5c0d878e6de'
        '0de8441c71735cd817c8d0c601ba848b1751c8c2d8f45b07baedf0b6e9061a8dba01e3cfca608232e8d78417bacac60dd1bce58125b698434e20da50e6b9723e')
validpgpkeys=(DD1EC9E8DE085C629B3E1846B18E8928B3948D64) # Michael Niedermayer <michael@niedermayer.cc>

prepare() {
  cd ffmpeg
  patch -Np1 -i ../add-av_stream_get_first_dts-for-chromium.patch # https://crbug.com/1251779
  patch -Np1 -i ../mathops-asm-fix.patch # https://trac.ffmpeg.org/ticket/10405
}

pkgver() {
  cd ffmpeg
  git describe --tags | sed 's/^n//'
}

build() {
  cd ffmpeg
  ./configure \
    --prefix=/usr \
    --disable-debug \
    --disable-static \
    --disable-stripping \
    --enable-amf \
    --enable-avisynth \
    --enable-lto \
    --enable-libfdk-aac \
    --enable-nonfree \
    --enable-fontconfig \
    --enable-gmp \
    --enable-gnutls \
    --enable-gpl \
    --enable-ladspa \
    --enable-libaom \
    --enable-libass \
    --enable-libbluray \
    --enable-libbs2b \
    --enable-libdav1d \
    --enable-libdrm \
    --enable-libfreetype \
    --enable-libfribidi \
    --enable-libgsm \
    --enable-libiec61883 \
    --enable-libjack \
    --enable-libjxl \
    --enable-libvpl \
    --enable-libmodplug \
    --enable-libmp3lame \
    --enable-libopencore_amrnb \
    --enable-libopencore_amrwb \
    --enable-libopenjpeg \
    --enable-libopenmpt \
    --enable-libopus \
    --enable-libpulse \
    --enable-librav1e \
    --enable-librsvg \
    --enable-libsoxr \
    --enable-libspeex \
    --enable-libsrt \
    --enable-libssh \
    --enable-libsvtav1 \
    --enable-libtheora \
    --enable-libv4l2 \
    --enable-libvidstab \
    --enable-libvmaf \
    --enable-libvorbis \
    --enable-libvpx \
    --enable-libwebp \
    --enable-libx264 \
    --enable-libx265 \
    --enable-libxcb \
    --enable-libxml2 \
    --enable-libxvid \
    --enable-libzimg \
    --enable-opencl \
    --enable-opengl \
    --enable-shared \
    --enable-version3 \
    --enable-vulkan
  make
  make tools/qt-faststart
  make doc/ff{mpeg,play}.1
}

package() {
  make DESTDIR="${pkgdir}" -C ffmpeg install install-man
  install -Dm 755 ffmpeg/tools/qt-faststart "${pkgdir}"/usr/bin/
}

# vim: ts=2 sw=2 et:
