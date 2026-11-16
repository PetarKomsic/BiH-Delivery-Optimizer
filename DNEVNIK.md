13.11.2026. - Početak rada na projektu
Odabir projekta:
	Odabran projekat A - Distribucija robe
Programski jezik:
	Python
Algoritmi:
	Planirani:
		- Simulated Annealing
		- Adaptive Large Neighborhood Search
		Potencijalne kasnije izmjene u slučaju prevelike kompleksnosti implementacije kvalitetnog ALNS algoritma

16.11.2026. - Lokacije i cestovne matrice
	- Poslovnice su izvezene iz OpenStreetMapa preko Overpass Turba. Izvoz bez limita dao je 159 zapisa. Na karti je potvrđeno da točka Maxi Konzuma u Ilijašu (node 2038703361) i obris zgrade (way 194066758) označavaju isti objekt, pa je zadržana točka s adresom. Ostalo je 158 kandidata. Kod dijela zapisa adresa nedostaje, pa uparivanje s Konzumovim službenim popisom ostaje za provjeru.
	- Za obje instance odabrana je stvarna adresa Kamenolom 10, Blažuj, Ilidža, kao polazište simulacije. Koordinate centra su 43.83524860448132, 18.264567158809943 (lat, lon). Konzum na adresi navodi sjedište i poslovnicu 0292.
	- openrouteservice Matrix API (profil driving-car) korišten je za cestovne udaljenosti u kilometrima i vremena u sekundama. Najprije je isproban zahtjev za tri točke. Prvi test prošao je na staroj adresi API-ja, a za daljnje zahtjeve korišten je api.heigit.org. Za 100 marketa i centar upit je podijeljen u četiri bloka.
	- Mala instanca spremljena je kao JSON odgovor, a velika kao dvije CSV matrice s ID-jevima polazišta i odredišta. Obje su provjerene. Svih 30 marketa i centar podudaraju se, a vrijednosti male instance jednake su odgovarajućim vrijednostima velike.
	- Ručna kontrola od centra do prvog marketa (42.9264605, 17.6152522): openrouteservice 186,29 km, Google Maps 196 km. Razlika je 9,71 km (oko 5 % u odnosu na Google Maps). Trase nisu uspoređene.
