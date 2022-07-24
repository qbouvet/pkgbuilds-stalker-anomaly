# Maintainer: Quentin Bouvet <qbouvet at outlook dot com>
pkgname="stalker-anomaly"
pkgver=1.5.2
pkgrel=1
pkgdesc="Standalone mod for S.T.A.L.K.E.R games series"
arch=('x86_64')
license=('none')
url="https://www.moddb.com/mods/stalker-anomaly"

depends=('wine' 'winetricks' 'unionfs-fuse')
makedepends=('p7zip') # 'rar2fs', 'fuse3-p7zip-git' 'innoextract' 'libguestfs'

source=(
  "file://${pkgname}"                   # /usr/bin wrapper script
  "file://${pkgname}.png"               # icon
  "file://${pkgname}.desktop"           # program shortcut
  "file://${pkgname}-launcher.desktop"  # launcher shortcut
  # https://www.moddb.com/downloads/stalker-anomaly-151
  "manual://Anomaly-1.5.1.7z"
  # https://www.moddb.com/mods/stalker-anomaly/downloads/stalker-anomaly-151-to-152
  "manual://Anomaly-1.5.1-to-1.5.2-Update.7z"
)
md5sums=(
  "SKIP"
  "SKIP"
  "SKIP"
  "SKIP"
  "0ee1e9a0e45c529536370ba76b0ec47f"
  "8f4d4000e8aee78f25ee2ac977acaa0f"
)
noextract=(
  "Anomaly-1.5.1.7z"
  "Anomaly-1.5.1-to-1.5.2-Update.7z"
)
install="${pkgname}.install"

# TODO: 
#   - Look into transmission-dlagent so that the pkgbuild can download the files directly
#     https://wiki.archlinux.org/title/PKGBUILD
#     https://aur.archlinux.org/packages/transmission-dlagent
#   - Take some inspiration from java jdk detecting source in /Downloads
#     https://aur.archlinux.org/cgit/aur.git/tree/PKGBUILD?h=jdk8


function notice() {
cat << EOF

PLEASE NOTE: FILES MUST BE MANUALLY DOWNLOADED: 
  - Anomaly-1.5.1.7z
    @https://www.moddb.com/downloads/stalker-anomaly-151
  - Anomaly-1.5.1-to-1.5.2-Update.7z
    @https://www.moddb.com/mods/stalker-anomaly/downloads/stalker-anomaly-151-to-152

PLEASE NOTE: THIS PACKAGE IS BIG: 
  - 10 GB of data will be downloaded
  - 25 GB of RAM / Swap will be used during build
  - The final package is ~17 GB in size

EOF
sleep 5
}

notice


#function prepare() {
#}


#function build() {
#}


function package() {

    cd "${srcdir}"    

    mkdir -p "${pkgdir}/usr/share/${pkgname}"

    # Extract archives directly to $srcdir  
    #   -o: output directory
    #   -ao: overwrite mode (a=all)
    7z x \
      -o"${pkgdir}/usr/share/${pkgname}/" \
      -ao'a' \
      'Anomaly-1.5.1.7z'
    7z x \
      -o"${pkgdir}/usr/share/${pkgname}/" \
      -ao'a' \
      'Anomaly-1.5.1-to-1.5.2-Update.7z'
    
    #   Set permissions
    find "$pkgdir"/usr/share -type f -exec chmod 644 "{}" \;
    find "$pkgdir"/usr/share -type d -exec chmod 755 "{}" \;
    
    #   Install binary wrapper / Icon / Desktop files
    install -m755 -D -t "${pkgdir}/usr/bin" \
      "${pkgname}"
    install -D -t "${pkgdir}/usr/share/icons/" \
      "${pkgname}.png"
    install -D -t "${pkgdir}/usr/share/applications/" \
      "${pkgname}.desktop"
    install -D -t "${pkgdir}/usr/share/applications/" \
      "${pkgname}-launcher.desktop"
}

#
# makepkg --printsrcinfo > .SRCINFO
#
