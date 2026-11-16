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

16.11.2026. - Logističke pretpostavke i početni rasporedi
	- Generirani su logistika_30.json i logistika_100.json sa seedom 16112026. ID-jevi povezuju datoteke s cestovnim matricama. Količine su u kg, vremena u sekundama, udaljenosti u kilometrima i valuta je BAM. Vrijeme vožnje po dionici za raspored zaokruženo je naviše na cijelu sekundu.
	- Radno vrijeme centra u simulaciji je 06:00–18:00. Kombi ima kapacitet 1.100 kg, fiksni trošak 45 BAM i 0,65 BAM/km. Kamion ima 4.500 kg, 90 BAM i 1,20 BAM/km. Flota uključuje jedno rezervno vozilo po tipu iznad broja vozila u početnom rasporedu.
	- Pristup samo kombijem simulira skučen prilaz i dodijeljen je dijelu marketa. Raspon je 150–600 kg za te markete i 250–1.500 kg za ostale. Istovar traje 8 minuta plus jedna minuta na svakih započetih 75 kg. Rute su konstruirane dodavanjem najbliže dostupne poslovnice po vremenu vožnje, uz kapacitet i povratak do 17:30. Termini su postavljeni oko planiranog početka istovara i zaokruženi na četvrt sata. Za ograničenje pristupa i troškove korištene su ilustrativne pretpostavke. Ista matrica driving-car koristi se za oba tipa vozila. Pauze vozača ostaju izvan osnovnog modela.
	- Ponovno su izračunati dolazak, početak i kraj istovara, povratak, teret, kilometraža i trošak za svaku rutu. Provjereni su jedinstvena posjeta, dopušteni tip vozila i raspoloživost flote. Mala instanca ima 9 ruta (3 kombija i 6 kamiona) i povratak najkasnije u 17:15:03. Velika ima 28 ruta (9 kombija i 19 kamiona) i povratak najkasnije u 17:18:37.
	- Usporedba cestovne i zračne udaljenosti za sve parove izdvojila je bliske OSM zapise 4684817291 i 4684952990. Razlika na kraćoj dionici je reda nekoliko metara ili manje i može ovisiti o točki na koju ih je servis spojio. Na karti još treba provjeriti jesu li to dvije odvojene poslovnice. Uparivanje poslovnica sa službenim popisom i dodatne ručne usporedbe ruta ostaju otvoreni.
	- Sljedeći korak je model u Pythonu, evaluator troška i validator ruta kao zajednička osnova za SA i ALNS.
