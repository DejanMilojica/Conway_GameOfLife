# Conway Game of Life!
## Kratak opis igre
Osmislio matematičar John Conway, Conwayova igra života (Conway Game of Life), je simulacijska igra, odnosno igra koja pokušava "simulirati" stvarne životne procese.
Simulacije se odvijaja matrici 10x10:
	Svaka ćelija (polje) u matrici može biti u jednom od dva moguća stanja: Živ ili Mrtav. Živo stanje predstavljeno "obojenim" poljem, dok je mrtvo stanje, praznim kvadratom.

 Svako polje, ima 8 susjednih/komsijskih polja(Isključujuci krajnja polja, koja imaju manje).

 Simulacija započinje postavljanjem pocetnih živih/mrtvih polja. To se naziva početna populaca. (Tehnički biste mogli započeti tako da su sve stanice mrtve, ali to bi učinilo dosadnu simulaciju.)
Početno stanje populacije, se preuzima iz datoteke "mapa.txt". Na taj način se omogucava korisnički odabir početnog stanja. Neka od zanimljivih pocetnih stanja, ce biti prilozena slikama!

 Takva populacija, se dalje kroz simulaciju razvija prema određenom skupu pravila. Skup pravila određuje šta se događa sa svakom ćelijom iz jedne generacije (konfiguracija živih i mrtvih ćelija) do druge.

 Pravila:
 - Polje živo, broj susjednih živih polja ,0 ili 1, u sljedećoj generaciji, ovo polje je mrtvo!
 - Broj susjednih živih polja jednak 2, polje zadrzava stanje!
 - Polje mrtvo, broj susjednih živih polja jednak 3, polje oživljava!
 - Broj susjednih živih polja 4 ili vise, polje mrtvo!

 Ukoliko simulaciju započnemo sa svim praznim poljima, takva ce i ostati. Ukoliko započnemo sa 1 ili 2 polja koji su zivi, simulacija će poživjeti samo jedan ciklus, jer će umrijeti usljed nedovoljnog susjedstva! Ukoliko zapocnemo sa punom matricom, u sljedecoj generaciji će ostati samo 4 krajnja polja. Početno stanje mozemo generisati i slučajno, ili proizvoljnim postavljanjem jedinica na zeljene pozicije.

### NAPOMENA!
	- Veća popunjenost matrice jedinicama, ne znaci da će simulacija duze trajati!

 Ono sto se pokazuje kao interesantno, je da započnemo sa nekim od vec poznatih sablona:

 <p align="center"> 
    <img src="./imgs/Sabloni.png" alt="Poznati Sabloni">
 </p>

## Realizacija:

 Realizacija se bazira na koriscenju C programskog jezika, odnosno <pthread.h> biblioteke, koja nam omogucava rad sa nitima. Svako polje/celija, predstavlja jednu programsku nit, pored glavne/main niti. Izvrsavanje niti se bazira na prioritetima.
 Svaka nit ima svoj prioritet. Prioriteti su prikazani na slici:

 <p align="center"> 
    <img src="./imgs/CGofLife.bmp" alt="Tabela Prioriteta">
 </p>

 Manja vrijednost, predstavlja veci prioritet, samim tim ima i "prednost" u izvrsavanju, u odnosu na ostale niti manjeg prioriteta!
 U skladu sa prethodnim, obezbedjuje se sljedce:
 Svako polje, zavisi od 8 susjednih polja, pri cemu gornja 3 polja, te lijevo polje, imaju veci prioritet, odnosno, moraju da se izvrse prije posmatranog polja. Na taj nacin se formira dijagonalna raspodjela prioriteta, kao sto se vidi na slici. Svako polje, koje ispunjava prethodni uslov, postaje konkurent za izvrsavanje. Evolucija polja koje se izvrsava, obavlja se po prethodno definisanim pravilima, uz uslov, da polje koje se izvrsava, uzima prethodna stanja polja vecih prioriteta, te trenutna stanja ostalih polja manjeg prioriteta.
 Generisanje prethodno pomenute tabele prioriteta, obavlja se u zavisnosti od veličine mape, koju program podržava. U skladu sa tim, promjena veličine mape, će izazvati formiranje dodatnih prioriteta.
## Izvrsavanje:

    PC / Raspberry PI


## Resursi:
 - https://home.adelphi.edu/~stemkoski/mathematrix/life.html
 - https://github.com/madelgi/game-of-life