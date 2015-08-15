# Maintainer: Jim Pryor <profjim@jimpryor.net>
# Warning: The chicken-* egg PKGBUILDS in AUR are auto-generated.
#          Please report errors you notice so that I can tweak the generation script.

pkgname=chicken-progress-indicators
pkgver=0.1
pkgrel=4
pkgdesc="Chicken Scheme Egg: text-mode progress-indicators"
arch=('i686' 'x86_64')
url="http://chicken.wiki.br/eggref/4/progress-indicators"
license=('unknown')
depends=('chicken>=4.5.0' 'chicken-defstruct' )
options=(docs !libtool !emptydirs)
install="chicken.install"
source=("$pkgname-$pkgver.chunked::http://chicken.kitten-technologies.co.uk/henrietta.cgi?name=progress-indicators&version=$pkgver"
		"$pkgname-$pkgver.html::http://chicken.wiki.br/eggref/4/progress-indicators.html")
md5sums=('568688175eb1ac1627a5d1030fc1fcca' '43631623c2654ffc61b6d1c65b164df3')

build() {
	# unchunk the blob that was downloaded from henrietta
	cd "$srcdir"
	mkdir -p "progress-indicators-$pkgver"
	cat "$pkgname-$pkgver.chunked" | while :; do
		while read -r bar ver endbar fname len; do
			[[ -n "$ver" ]] && break
		done
		[[ "$endbar" = "|#" ]] || fname="$ver" len="$endbar"
		[[ -z "$fname" ]] && break
		fname="${fname:1:${#fname}-2}" # delete quotes around fname
		if [[ "${fname: -1}" == / ]]; then
			mkdir -p "progress-indicators-$pkgver/$fname"
		elif [[ "$len" -eq 0 ]]; then
			touch "progress-indicators-$pkgver/$fname"
		else
			dd iflag=fullblock of="progress-indicators-$pkgver/$fname" ibs="$len" count=1 2>/dev/null
		fi
	done
	

	cd "$srcdir/progress-indicators-$pkgver"
	cp ../$pkgname-$pkgver.html progress-indicators.html
	
	
	mkdir -p "$pkgdir/usr/lib/chicken/5" "$pkgdir/usr/share/chicken/progress-indicators"
		
	chicken-install -p "$pkgdir/usr"
	
		install -Dm644 "progress-indicators.html" "$pkgdir/usr/share/doc/$pkgname/progress-indicators.html"
}
