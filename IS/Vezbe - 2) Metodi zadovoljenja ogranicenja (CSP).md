U standardnim algoritmima pretraživanja: 
-  Stanje je „crna kutija“. Postoji startno stanje, ciljno stanje i ostala stanja u koja se u procesu pretraživanja može dospeti. 
- Operatori/akcije omogućavaju prelazak iz jednog u drugo stanje.
- Test cilja proverava da li je trenutno stanje jedno od ciljnih stanja. 

U metodima zadovoljenja ograničenja: 
- Stanje se definiše promenljivama Xi koje mogu uzimati vrednosti iz domena Di.
- Test cilja proverava da li su dodeljene vrednosti svakoj od promenljivih u skladu sa ograničenjima nametnutih od strane samog problema, tj. da li su nametnuta ograničenja zadovoljena (konzistentna dodela).

# Hillclimbing pretraga

Hillclimbing je vrsta lokalne pretrage, koja se moze primeniti u resavanju CSP problema. Na pocetku se svim promenljivima na odredjen nacin dodeli pocetna vrednost iz njihovih domena i takvo stanje se proglasava startno.

Startno stanje predstavlja potpunu dodelu koja ignorise ogranicenja nemtnuta problemom.

Zatim se na osnovu startnog stanja generiše novo susedno stanje izborom promenljive koja ima nerazrešena ograničenja sa drugim promenljivama i izborom vrednosti za tu promenljivu tako da novo stanje bude bolje od trenutnog. Može se težiti tome da novo stanje bude najbolje od svih mogućih susednih stanja trenutnog stanja, ali ne mora nužno, već je dovoljno da je bolje od trenutnog stanja. Novo stanje se proglašava za trenutno.

Posto moze da se desi da ne postoje vide bolja stanja od trenutno, ali to trenutno nije dobro resenje mi odajemo novu ideju u algoritam koja omogucava algoritmu da izabere gore stanje od trenutnog u cilju nalazenja resenja.

Simulate annealing je vrsta lokalne pretrage, koja dodaje jednu vrednost "temperatura" koja se menja tokom rada algoritma. Kada napravimo dobar korak ona se poveca, a kada se vratimo u neoptimalno stanje mi ga smanjujemo. Time dajemo algoritmu lufta da pravi neoptimalne korake da bi nasao dobro resenje.

# Backtracking pretraga

Backtracking je obicna [[Vezbe - 1) Prostor i algoritmi pretrazivanja#DFS - Depth First Search|DFS]] ptretraga.

Stanje u problemu se definise dodelama vrednosti promenljivima. Inicijalno stanje je prazna dodela.

Funkcija prelaza iz stanja u stanje vrši dodelu vrednosti jednoj od promenljivih koja nema dodeljenu vrednost. Takva dodela ne sme da krši nijedno ograničenje nametnuto samim problemom. Ukoliko takva dodela ne postoji, onda je neophodno vratiti se korak unazad (backtrack) i promeniti dodeljenu vrednost prethodnoj promenljivoj kojoj je vrednost dodeljena ili vratiti se na prethodnu promenljivu, ukoliko su isprobane sve vrednosti.

Poboljsanje ovog algoritma je ako umesto da idemo korak po korak da prvo ciljamo na promeljivu sa najvecim brojem ogranicenja. Ideja je da zavrsimo pogresnu pretragu sto pre. Ukoliko ima vise takvih promenljiva onda izabrati onu sa najvecim brojem ogranicenja. 

Sada kada smo odabrali promenljivu biramo onu vrednost sa sto manje ogranicenjima u sebe.


```handdrawn-ink
{
	"versionAtEmbed": "0.2.6",
	"filepath": "a PNG folder/Ink/Drawing/2024.10.24 - 1.23am.drawing"
}
```
# Forward Checking

