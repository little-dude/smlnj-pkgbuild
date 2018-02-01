# Maintainer: Corentin Henry <corentinhenry@gmail.com>
pkgname=smlnj
pkgver=110.82
pkgrel=1
pkgdesc="Standard ML of New Jersey compiler and libraries"
arch=('x86_64')
url="http://www.smlnj.org"
license=('custom')
groups=()
depends=("lib32-glibc")
makedepends=("lib32-gcc-libs")
optdepends=()
provides=()
conflicts=()
replaces=()
backup=()
options=()
install=
changelog=

_url="http://smlnj.cs.uchicago.edu/dist/working/$pkgver/"
_files=("boot.x86-unix.tgz"
        "config.tgz"
        "cm.tgz"
        "compiler.tgz"
        "runtime.tgz"
        "system.tgz"
        "MLRISC.tgz"
        "smlnj-lib.tgz"
        "old-basis.tgz"
        "ckit.tgz"
        "nlffi.tgz"
        "cml.tgz"
        "eXene.tgz"
        "ml-lpt.tgz"
        "ml-lex.tgz"
        "ml-yacc.tgz"
        "ml-burg.tgz"
        "pgraph.tgz"
        "trace-debug-profile.tgz"
        "heap2asm.tgz"
        "smlnj-c.tgz"
        "doc.tgz")
source=("LICENSE")
noextract=()
for f in "${_files[@]}" ; do
    source+=("${_url}/${f}")
    if [ "${f}" != "config.tgz" ] ; then
        noextract+=("${f}")
    fi
done
md5sums=('fdd45f0ec2fa0006357baece04d7e0d0'
         'dc5c8510481b68f57d378ceff2e74cdc'
         'adeea40c1b9afdb1d58daca29f835141'
         'e356d5398eb7aa01d0dc21ec63337311'
         '17295ddfbab3280ac971db5983fe61f0'
         '983e31b9284c89e9cd0b5dfab6e6729c'
         '314468cf57feba89ccc1ca9c33b72b45'
         '8e0a0b056f20446a7c8326ef5c84323d'
         'ac339808917e2fd1756b4f38ce7f9afb'
         'dd1533f05805a3fe5f8d7d9f672d186c'
         '234387df3d86b3f5d63b3344caa0cae6'
         '97c3fc8f31f6b0e7af9cbd60bdff06e4'
         '047e1665dcc7f7bf2396a1647ceceac9'
         '9d71cf2723f989cb8a32e50f1eb4ea51'
         '0083d3ba51ce4c1c126a9df02116a468'
         'c563f1890867f2a2daf677e83b30653f'
         'e6eab43e7b6c57cbeddeb2ddfc3e8c03'
         '11d83ed2d1857d63b6818c0368a5280c'
         '0c05be23dadfa27315a103401fe79544'
         '4aad83751116abf4f8f27a6a9617018b'
         '0fe17e3209a398811377a3836721bb0a'
         '3a66a72c756691054a3e986dc1736af9'
         '0f8f0bd3f6f9e91fdd5ba923b33e79ec')

prepare() {
    # Prevent smlnj build script to download anything
    # Downloading files is done by makepkg
    echo "SRCARCHIVEURL=\"file:/${srcdir}\"" > config/srcarchiveurl
}

build() {
    ./config/install.sh
}

package() {
    install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
    cp -r bin lib ${pkgdir}/usr/
    for file in "${pkgdir}"/usr/bin/*; do
        # sed does some magic on the links here.
        # See https://unix.stackexchange.com/a/192017/45689 to understand why this works
        [[ -f ${file} ]] && sed "2iSMLNJ_HOME=/usr" -i ${file}
    done
}
