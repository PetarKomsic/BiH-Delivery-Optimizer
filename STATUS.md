Početak rada: 13.11.2026.
Trenutna faza: Priprema modela i algoritama
Rok: 4 sedmice(okvirno)
Odbrana: Nepoznat datum

Završeno:
	- Odabran projekt
	- Napravljen github repozitorij
	- Postavljeno virtuelno okruženje
	- napravljeni README, STATUS i DNEVNIK
	- Prikupljeno 158 kandidata iz OpenStreetMapa nakon uklanjanja jednog potvrđenog duplikata.
	- Odabrana lokacija centra za simulaciju na adresi Kamenolom 10, Blažuj, Ilidža.
	- Izračunate i provjerene probne matrice za 30 i 100 marketa, s istim centrom. Matrice su 31 × 31 i 101 × 101, bez nedostajućih vrijednosti. Mala matrica podudara se s odgovarajućim dijelom velike.
	- Generirani `logistika_30.json` i `logistika_100.json`. Ponovno su provjereni prema cestovnim matricama. Početni rasporedi imaju 9 i 28 dopustivih ruta.

Planirano:
	- Sljedeća sesija: učitati instance u Pythonu, napisati evaluator troška i validator ruta, pa krenuti sa Simulated Annealingom i ALNS-om.
	- Provjeriti odabrane OSM lokacije prema službenom popisu Konzuma i provjeriti još nekoliko cestovnih ruta.
	- Ujednačiti format matrica i spremiti podatke s opisom izvora, jedinica i identifikatora.
	- Odabrati najmanje šest benchmark instanci i zabilježiti izvore i objavljene rezultate.
	- Pravljenje osnovnog plana rada, i podjela na faze
