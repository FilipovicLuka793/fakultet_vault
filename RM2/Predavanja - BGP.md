
# CDN - Content Delivery Network 

Uloga je prenos web, multimedia, live sadzaja. kako je pre radilo je klijent posalje zahtev za nekim medijima i onda server ih salje, a kada drugi korisnik uputi isti upit drugi server salje podatke tom korisniku. Medjutim sada bottleneck postaje mreza i ona moze biti zagusena. Tako je nastala CDN ideja koja je da ne postoji vise servera na jednom mestu vec da zu ti serveri razbacani po citavom internetu i u svakom serveru se nalaze potrebni podaci. Time mreza nece biti zagusena.


```handdrawn-ink
{
	"versionAtEmbed": "0.2.6",
	"filepath": "a PNG folder/Ink/Drawing/2024.10.19 - 16.57pm.drawing"
}
```
```handdrawn-ink
{
	"versionAtEmbed": "0.2.6",
	"filepath": "a PNG folder/Ink/Drawing/2024.10.19 - 16.59pm.drawing"
}
```
![[Pasted image 20241019171606.png]]
1. Korsink trazi od DNS servera da mu da IP adresu za sajt "www.sadrzaj.com"
2. DNS sad to salje CDN DNS serveru koji sada nalazi optimalni put do tog sajta.
3. CDN DNS server je nasao optimalan put i IP adresu salje DNS serveru
4. DNS server salje dobijenu IP adresu do korisnika
5. Browser korisnika uzima tu adresu i salje GET zahtev ka toj adresi.
6. Lokalbni CDN server zadrziji kopije sadrzaja i ako su u njemu kesirani podaci on ce da posalje podatke korisniku, a ako nisu zahtev ce traziti od originalnog servera
7. Kada zahtev stigne do originalnog servera od salje Lokalnom CDN serveru koji kesira te podatke
8. I na kraju salje to korisniku

Ovim postupkom je obezbedjen minimalni kontakt sa glavnom mrezom koja je povezana ka originalnom podatku vec se ti podaci skladiste na lokalnom serveru i time se ne opterecuje mreza.

# BGP

Atonomni sistem (AS) je skup uredjaja i veza koji su pod odredjenom administrativnom kontrolom.

BGP sluzi za razmenu ruta izmedju autonomnih sistema. Protokol rutiranja imazi zadatak da obezbede prosledjivanje paketa tehnicki najekonomicnijom putanjom.

![[Pasted image 20241019174621.png]]

![[Pasted image 20241020171510.png]]

AS sa jednim izlazom moze koristi default rutu sto znaci da korisnik ima jednu jedinu rutu kojoj upucuje zahtev kada hoce da se poveze na internet.

<span style="color:rgb(255, 0, 0)">Ovaj oblik AS se ne koristi u praksi!!!</span> 

![[Pasted image 20241020171912.png]]

As sa vise izlaza bez tranzita su korisnici koji imaju u interesu da pruzaju neku uslugu internetu ali nije im u interesu da propustaju drugi saobrazaj kroz njihovu mrezu. To rade tako sto kada su povezani na vise internet providera oni ruterima providera salju svoju ip adresu za servere i  ta internet veza radi isto. Medjuti kada se prikljuci neka druga veza za tog korisnika ona dobije ip adresu servera ali ne i ip adresu prvobitne mreze koja se povezala na taj servis. Time se sprecava da ruteri uopste znaju jedan za drugog i ne mogu da koriste servere korisnika za jnihovu medjusbnu komunikaciju.

![[Pasted image 20241020173112.png]]

Sada postoji tranzit smedju veze X i Y i mogu da koriste servere korisnika za komunikaciju.

<span style="color:rgb(255, 0, 0)">Bitna razlika izmedju Rooting protokola i BGP-a je to sto postoji filtriranje IP adresa.</span> 

BGP moze da se korisi:
* izvan AS-a i onda je ekterni BGP - EBGP
* unutar AS-a i onda je interni BGP - IBGP

BGP se ne koristi:
- Kada postoji samo jena veza sa internetom ili ISP
- Kada je politika mreze ista kao ISP rutiranje
- Granicni ruteri se podrzavaju ili nemaju dovoljno resursa za BGP
- Mali propusni opseg izmedju 2 mreze

<span style="color:rgb(255, 0, 0)">BGP koristi TCP za razmenu svojih poruka!!!</span>

Postoje nekoliko tipa poruka u BGP a to su:
- Open - ona otvara konekciju
- Notification - ako postoji neslaganje parametara i ne moze da se uspostavi veza
- Update - ruteri razmenjuju sve poznate rute
- Update - kada se promeni ruting tabela ova vrsta poruke se salje
- Keepalive - ako neko vreme nema razmene informacija salje se ova poruka da se proveri stanje

![[Pasted image 20241020190618.png]]

![[Pasted image 20241020191231.png]]

# EBGP i IBGP

![[Pasted image 20241020192120.png]]

Karakteristika BGP rutera je da ako imamo u neki AS poruku X i zelimo da je posaljemo u neki drugi AS, ona ce da se prenese pomocu EBGP-a i taj ruter koji ju je primio ce da je prosledi IBGP-om do granicnih rutera. Medjutim ti granicni ruteri koji su je dobili na rutere koji su povezani IBGP vezom nece da im posalje tu poruku koju su primili. To je suprotno od onoga sto se desava u RIP protokolu.

![[Pasted image 20241020195247.png]]

Ovde postoji problem kada AS1 hoce da posalje paket AS3 posto nije uspostavljena sinhronizacija. Ovaj problem se resava tako sto na putanji do destinacionog rutera u AS2 mora da se uspostavi podpun graf IBGP sesija. Tek tada sme da se salju paketi kada je graf uspostavljen.

![[Pasted image 20241020195604.png]]

# Path attributes

Atributi se dele u 4 grupe:
- Well-known mandatory - Dobro poznati atributi koji moraju da psotoje da bi bila BGP rutireanje
- Well-know discretionary - Dobro poznati atributi koji nisu neophodni da se implementiraju
- Optional transitive - Ne moraju da se poznaju i posto su tranzitivni nije bitno da li sledeci ruter zna za njegovo postojanje
- Oprinal nontransitive - Ne moraju da se prepoznaju ali sledeci rute ga nece prepoznati ako ne bude znao za tu opciju

![[Pasted image 20241021015257.png]]

Proces izbora najbolje rute u BGP protokolu rutiranja:
1. Ako Next Hop atribut za datu rutu ne postoji u ruting tabeli, ruta se ignoriše tj ne ubacuje u ruting tabelu.
2. Ako su Weight vrednosti iste, u ruting tabelu ulazi ruta sa najvećom vrednošću Local Preference.
3. Ako su prethodni kriterijumi isti, u ruting tabelu ulazi ruta sa kraćim AS-Path-om.
4. Ako su AS-Path dužine iste, ruter će odabrati rutu sa nižom vrednošću Origin atributa.
5. Ako je i to isto, Ruter će odabrati rutu sa nižom MED vrednošću.
6. Ako su i MED vrednosti iste, ruter će da odabere prvo rute čije putanje idu preko EBGP konekcija u odnosu na dobijene iz IBGP konekcija.
7. Bira se ruta čija je IGP metrika do BGP Next hopa niža.
8. Ako su prethodni kriterijumi isti, bira se ruta koja je dobijena ranije (prva koja je stigla u ruter).
## Next Hop Atribut (Obavezni)

U <span style="color:rgb(0, 176, 240)">EBGP</span> sesijama, next hop je IP adresa EBGP suseda koji je oglasio.

![[Pasted image 20241021123415.png]]

U <span style="color:rgb(0, 176, 240)">IBGP</span> sesijama, ako su rute oglasene unutar samog AS, next hop je OP adresa rutera unutar AS koji je oglasio datu rutu.

![[Pasted image 20241021123739.png]]

U <span style="color:rgb(0, 176, 240)">IBGP</span> sesijam, ako rute oglasene u AS iz nekog drugog AS putem EBGP, next hop koji je dobijen putem EBGP se unosi nepromenjen u IBGP.

![[Pasted image 20241021124032.png]]

**Next hop na Multiaccess segmentima:**

![[Pasted image 20241021125037.png]]

Ovo je specificna situacije gde RTB hoce da uspostavi sesiju sa RTA i po pravilo RTA ce da dobije IP adresu RTC. Medjuti posto ima direktna veza sa RTB bez potrebe da se ide preko RTC, RTC ce da posalje IP adresu RTB da bi dalje slanje podataka bilo efikasnije i brze.

## AS_Path Atribut (Obavezni)

![[Pasted image 20241021125829.png]]

AS_Path funkcionise na sledeci nacin. Kada neki autonomni sistem uspostavljam sesiju sa drugim autonomnim sistemom on uz Next Hop dodaje iz broj svog AS-a. Taj autonomni sistem koji je dobio taj broj on na to doda svoj broj AS-a i propagira dalje. To se sve radi do trenutka kada se desi da AS detektuje svoj broj AS-a medju tim brojevima gde se ta veza onda terminise.

<span style="color:rgb(255, 0, 0)">Ovo je osnovni nacin kako se sprecavaju petlje u BGP-u.</span> 

Da bi se nasla optimalna putanja AS_Path se pusta vise puta kroz razlicite putanje da bi se nasla najbolja putanja.

Takodje unutar IBGP-a ulazna adresa koja se dobila nece promeniti, vec se broj AS-a dodaje tek posto se ta adresa propagira na drugi AS.

Postoji i AS_Path prepending koja ustvari znaci da moze neka ruta da se pokvari ako zelimo da bi se postigle bolje performanse.

![[Pasted image 20241021131005.png]]

Konkretno u ovom priperu smo na levu rutu dodali 3 puta 700 da bi namestili da ta ruta bila duza i samim tim posto je duza BGP nece je izabrati kao optimalnom rutom.

Kada se povezuje na internet AS_Path mora da se izbrise radi privatnosti.

![[Pasted image 20241021134909.png]]

## Origin Atribut (Obavezni)

Origin atribut govori o poreklu rute. Koristi se za izbor najbolje rute. Vrste origin atributa:
- IGP - Prefiks je dobijen iz IGP iz datog AS
- EGP - Prefiks je dobijen iz EGP
- Incomplete - Prefiks je dobijen redistribucijom

Redosled prioritera je sledeci: IGP < EGP < Incomplete

## Atomic aggregate Atribute (Nisu obavezni)

Koristi se kod agregacije ruta i oznacava gubitak informacija u AS_Path atributa. 

Moze da ima vrednost True ili False.

![[Pasted image 20241021140651.png]]

## The Aggregator Atribut (Opcioni tranzitivni)

Ovim atributom se oznacava onaj ruter koji je izvrsio agregaciju ruta.

Kao argument ovog atributa upisuje se Router ID rutera koji je izvrsio agregaciju.

## AS_Set (Opcioni tranzitivni)

Kada se vrsi agregacija neke rute AS_Set pomaze u zadrzavanju informacija koje se izgube prilikom agregacije.

![[Pasted image 20241021141130.png]]

## Local Preferences Atribut (Nisu obavezni)

Oznacava stepen prioriteta za datu rutu. U ruting tabelu se ubacuje ona ruta koja ima visi Local Preference.

Local Preference, je lokalna za jedan AS.

<span style="color:rgb(255, 0, 0)">Local preference se odnosi na saobracaj koji izlazi iz datog AS!!!</span>

![[Pasted image 20241021144804.png]]

## Mutiple Exit Discriminator - MED (Opcioni netranzitivni)

On je suprotan od Local Preference zato sto on dodeljuje metriku ruta koje izlaze iz AS-a. Prioritet imaju rute sa manjom metricom.

![[Pasted image 20241021145820.png]]

MED atribut je netranzitivan sto znaci da putanja ne moze da se prosledjuje kroz druge AS vec samo vazi za susede.

![[Pasted image 20241021150210.png]]

## Weight Atribut

![[Pasted image 20241021150833.png]]

## Atribut Community (Opcioni tranzitivni)




