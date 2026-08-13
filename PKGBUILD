# Maintainer: acd407 <acd407@localhost>
pkgname=alsa-ucm-cros-redrix
pkgver=1.0
pkgrel=2
pkgdesc="ChromeOS UCM configs for Google Redrix (sof-rt5682) audio card"
arch=('any')
url="https://github.com/WeirdTreeThing/alsa-ucm-conf-cros"
license=('BSD')
source=()
md5sums=()

package() {
  _dest="$pkgdir/usr/share/alsa/ucm2"
  install -Dm644 "$startdir/platforms/intel-sof/platform.conf" "$_dest/platforms/intel-sof/platform.conf"
  install -Dm644 "$startdir/platforms/intel-sof/codecs.conf"   "$_dest/platforms/intel-sof/codecs.conf"
  install -Dm644 "$startdir/codecs/max98390/init.conf"        "$_dest/codecs/max98390/init.conf"
  install -Dm644 "$startdir/codecs/max98390/speaker.conf"     "$_dest/codecs/max98390/speaker.conf"
  install -Dm644 "$startdir/codecs/hda/hdmi2345.conf"         "$_dest/codecs/hda/hdmi2345.conf"
  install -Dm644 "$startdir/codecs/rt5682s/init.conf"         "$_dest/codecs/rt5682s/init.conf"
  install -Dm644 "$startdir/codecs/rt5682s/headset.conf"      "$_dest/codecs/rt5682s/headset.conf"
  install -Dm644 "$startdir/conf.d/sof-rt5682/sof-rt5682.conf"      "$_dest/conf.d/sof-rt5682/sof-rt5682.conf"
  install -Dm644 "$startdir/conf.d/sof-rt5682/HiFi.conf"            "$_dest/conf.d/sof-rt5682/HiFi.conf"
  install -Dm644 "$startdir/conf.d/sof-rt5682/rt5682-init.conf"     "$_dest/conf.d/sof-rt5682/rt5682-init.conf"
  install -Dm644 "$startdir/conf.d/sof-rt5682/rt5682-headset.conf"  "$_dest/conf.d/sof-rt5682/rt5682-headset.conf"
}