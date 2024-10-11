### 1.1 Deterministicki konacni automati
![[Pasted image 20241006004612.png]]
![[Pasted image 20241006004629.png]]

![[Pasted image 20241006004842.png]]
Suvisna stanja su stanja do kojih je nemoguce doci. Ovo ce mo odrediti pomocu skupa D u kojima se nalaze samo elementi do kojih mozemo doci.

1. D = {A}
2. D = {<span style="color:rgb(255, 0, 0)">A</span>, C, E, G}
3. D = {<span style="color:rgb(255, 0, 0)">A</span>, <span style="color:rgb(255, 0, 0)">C</span>, E, G, J, H}
4. D = {<span style="color:rgb(255, 0, 0)">A</span>, <span style="color:rgb(255, 0, 0)">C</span>, <span style="color:rgb(255, 0, 0)">E</span>, G, J, H}
5. D = {<span style="color:rgb(255, 0, 0)">A</span>, <span style="color:rgb(255, 0, 0)">C</span>, <span style="color:rgb(255, 0, 0)">E</span>, <span style="color:rgb(255, 0, 0)">G</span>, J, H}
6. D = {<span style="color:rgb(255, 0, 0)">A</span>, <span style="color:rgb(255, 0, 0)">C</span>, <span style="color:rgb(255, 0, 0)">E</span>, <span style="color:rgb(255, 0, 0)">G</span>, <span style="color:rgb(255, 0, 0)">J</span>, H, B}
7. D = {<span style="color:rgb(255, 0, 0)">A</span>, <span style="color:rgb(255, 0, 0)">C</span>, <span style="color:rgb(255, 0, 0)">E</span>, <span style="color:rgb(255, 0, 0)">G</span>, <span style="color:rgb(255, 0, 0)">J</span>, <span style="color:rgb(255, 0, 0)">H</span>, B}
8. D = {<span style="color:rgb(255, 0, 0)">A</span>, <span style="color:rgb(255, 0, 0)">C</span>, <span style="color:rgb(255, 0, 0)">E</span>, <span style="color:rgb(255, 0, 0)">G</span>, <span style="color:rgb(255, 0, 0)">J</span>, <span style="color:rgb(255, 0, 0)">H</span>, <span style="color:rgb(255, 0, 0)">B</span>}

Zakljucujemo da jedino elementi {D, F, I} nisu u ovom skupu znaci oni su visak.

![[Pasted image 20241006005357.png]]

![[Pasted image 20241006092536.png]]
Stanje S$x$ automata X <span style="color:rgb(255, 0, 0)">ekvivalentno</span> je stanju S$y$ automata Y ako i samo ako automata X startujucu od stanja S$x$ prihvata tacno isti skup sekvenci kao i automat Y statujuci od stanja S$y$.

Stanja S$x$ i S$y$ su ekvivalentna ako i samo ako su zadovoljeni:
1. *Uslov kompatibilnosti* - stanja S$x$ i S$y$ moraju oba biti ili stanja prihvatanja ili stanja odbijanja.
2. *Uslov propagacije* - prelazi iz ovih stanja za svaki ulazni simbol, moraju biti u medjusobno ekvivalenta stanja.
<span style="color:rgb(255, 0, 0)">Dva stanja su ekvivalentna</span> ako i samo ako su im startna stanja ekvivalentna.
![[Pasted image 20241006094515.png]]

- Da bi vazilo M <=> N treba da bude A1 <=> A2.
- A1 je kompitabilno sa A2 (oba stanja odbijanja).

![[Pasted image 20241006094654.png]]

- Da bi A1 <=> A2 treba da bude B1 <=> C2, kao i C1 <=> C2. Kompatibilnost je uredu tako da sada moramo da propagiramo.

![[Pasted image 20241006094841.png]]

- Nema nekompatibilnih stanja => svi parovi iz tabele predstavljaju medjusobno ekvivalentna stanja

![[Pasted image 20241006095227.png]]

![[Pasted image 20241006124911.png]]

<span style="color:rgb(255, 0, 0)">Ekvivalentan automat</span> je onaj koji prihvata tacno isti skup sekvenci kao i polazni automat. Takav automat nema suvisnih niti medjusobnog ekvivalentnih stanja.

Postupak:
1. uklanjanje suvusnih stanja
2. nalazenje skupova medjusobno ekvivalentih stanja.

Prvi koraj je eliministanje suvisnih stanja: D = {S1, S3, S5, S6, S7, S4} znaci da je stanje S2 suvisno.

Sada se prati sledeci algoritam:
1. Inicijalno podela na stanja prihvatanja i stanja odbijanja:

		P0 = ({S1, S3, S5, S7}, {S4, S6})

2. U narednim koracima pokušavamo da dalje razbijemo pojedine skupove stanja, utvrđujući koja stanja ne zadovoljavaju uslov propagacije. Prvo ćemo razmotriti skup stanja {S1, S3, S5, S7} i prelaz iz ovih stanja za ulazni simbol 0:

![[Pasted image 20241006125621.png]]

S3 treba izdvojiti jer njegov prelaz je u drugi skup. Tako imamo drugu podelu:

	P1 = ({S1, S5, S7}, {S3}, {S4, S6})

Isto se ponavlja i za ostale skupove:

![[Pasted image 20241006125918.png]]

	P2 = ({S1, S7}, {S5}, {S3}, {S4, S6})

Isto se radi i za skup {S4, S6} ali tu nece biti promena.

	A = {S1, S7}
	B = {S4, S6}
	C = {S3}
	D = {S5}

Dakle rezultirajuci minimalni automat je:

![[Pasted image 20241006130515.png]]

Do ove tabele smo dosli tako sto smo testirali za svaki skup sa ulazima 0 i 1 u koji drugi skup se krecu:

![[Pasted image 20241006130939.png]]

### 1.2 Nedeterministicki konacni automati

![[Pasted image 20241006131157.png]]

![[Pasted image 20241006131350.png]]

Po definiciji, ako postoji bar jedan scenario prihvatanja sekvenca se prihvata.

|     |            |     a      |     b      |    c    |
| :-: | :--------: | :--------: | :--------: | :-----: |
| S0  |  A, B, C   | A, B, C, E |  A, B, C   |  D, E   |
| S1  | A, B, C, E | A, B, C, E | A, B, C, E |  D, E   |
| S2  |    D, E    |    D, E    |    D, E    | A, B, E |
| S3  |  A, B, E   | A, B, C, E |  A, C, E   |    E    |
| S4  |  A, C, E   | A, B, C, E |  B, C, E   |  D, E   |
| S5  |     E      |     E      |     E      |    E    |
| S6  |  B, C, E   |  A, C, E   | A, B, C, E |  D, E   |
Svaki skup koji u sebi sadrzi C je stanje prihvatanja.

![[Pasted image 20241011112859.png]]

Sva prazna polja oznacavaju stanje greske tako da se ta polja ignorisu. Kako startujemo ovaj algoritam je u prvi skup $S_{0}$ izaberemo sva stanja moja mogu da budu pocetna. U ovom slucaju to su A i C. Zatim za svaki ulaz gledamo sta ce da se desi i generisemo nove skupove na osnovu ulaznog simbola.

![[Pasted image 20241011113347.png]]

$S_{0}=\{A, C\}$
$S_{1}=\{A, D\}$
$S_{2}=\{C, D\}$
$S_{3}=\{A\}$
$S_{4}=\{C\}$
$S_{5}=\{D\}$

Ako skupove napisemo u ovom obliku dobijamo DKA:


|         | x       | y       | z       |     |
| ------- | ------- | ------- | ------- | --- |
| $S_{0}$ | $S_{1}$ | $S_{2}$ | $S_{3}$ | 1   |
| $S_{1}$ | $S_{1}$ | $S_{4}$ | $S_{3}$ | 1   |
| $S_{2}$ | $S_{5}$ | $S_{2}$ | $S_{3}$ | 1   |
| $S_{3}$ | $S_{1}$ | $S_{4}$ | $S_{3}$ | 0   |
| $S_{4}$ |         | $S_{2}$ |         | 1   |
| $S_{5}$ | $S_{5}$ | $S_{4}$ | $S_{3}$ | 1   |
Stanje prihvatanja se bira tako sto ako u tom skupu se nalazi element koji u originalnom NKA bio stanje prihvatanja onda je i taj skup u kome se on nalazi stanje prihvatanja.

![[Pasted image 20241011143910.png]]


| NKA                                         | a    | b    | c   |     |
| ------------------------------------------- | ---- | ---- | --- | --- |
| <span style="color:rgb(255, 0, 0)">0</span> | 1    |      |     | 0   |
| 1                                           | 2, A | 1    |     | 0   |
| 2                                           |      | 0, A |     | 0   |
| <span style="color:rgb(255, 0, 0)">A</span> |      | B    | C   | 0   |
| B                                           |      | C    |     | 1   |
| C                                           |      |      | A   | 0   |
<span style="color:rgb(255, 0, 0)">Crvena</span> - moguca pocetna stanja

Nula moze da bude pocetak sekvence posto je on pocetak sekvence iz prve tabele a znamo da sekvenca mora da pocen iz te tabele. A je takodje pocetak sekvence posto kao sto vidimo iz tabele a) nula je stanje prihvatanja sto znaci da je validno da predjemo na sledecu tabelu bez bilo kod drugog znaka sto znaci da moze i da bude prazna sekvenca.

U NKA tabeli stanja prihvatanja i odbijanja smo odredili tako sto znamo da mora prvo da ide sekvenca iz tabele a) pa tek onda sekvenca iz tabele b) sto automatcki znaci da nijedno stanje iz tabele a) ne moze da bude stanje prihvatanja, a sva stanja iz tabele b) su identicne.

U NKA tabeli u stanju 1 i 2 je takodje napisan ( , A ) sto oznacava da kada dodje simbol iz te kolone moguce je uci u tabelu b).

Sada kada imamo NKA mozemo na osnovu nje da odredimo DKA:


| DKA               | a               | b                 | c             |     |
| ----------------- | --------------- | ----------------- | ------------- | --- |
| $S_{0}=\{0,A\}$   | $S_{1}=\{1\}$   | $S_{2}=\{B\}$     | $S_{3}=\{C\}$ | 0   |
| $S_{1}=\{1\}$     | $S_{4}=\{2,A\}$ | $S_{1}=\{1\}$     |               | 0   |
| $S_{2}=\{B\}$     |                 | $S_{3}=\{C\}$     |               | 1   |
| $S_{3}=\{C\}$     |                 |                   | $S_{5}=\{A\}$ | 0   |
| $S_{4}=\{2,A\}$   |                 | $S_{6}=\{0,A,B\}$ | $S_{3}=\{C\}$ | 0   |
| $S_{5}=\{A\}$     |                 | $S_{2}=\{B\}$     | $S_{3}=\{C\}$ | 0   |
| $S_{6}=\{0,A,B\}$ | $S_{1}=\{1\}$   | $S_{7}=\{B,C\}$   | $S_{3}=\{C\}$ | 1   |
| $S_{7}=\{B,C\}$   |                 | $S_{3}=\{C\}$     | $S_{5}=\{A\}$ | 1   |

### 1.3 Regularni izrazi

![[Pasted image 20241011145923.png]]

Bitno zapamtiti ==> [[Predavanja - 2) Leksicka analiza#Konstrukcija konacnog automata iz regularnog izraza]]

![[Pasted image 20241011151433.png]]

![[Pasted image 20241011151448.png]]

c)

|                                 | +   | -   | *   | d   |     |
| ------------------------------- | --- | --- | --- | --- | --- |
| A = {1, 2, 4, 6, 7, 8, 9}       | B   | C   |     | E   | 0   |
| B = {3, 8, 9}                   |     |     |     | E   | 0   |
| C = {5, 8, 9}                   |     |     |     | E   | 0   |
| E = {9, 10, 11, 12, 17, 18, 19} |     |     | F   | E   | 1   |
| F = {13, 14}                    |     |     |     | G   | 0   |
| G = {14, 15, 16, 19}            |     |     |     | G   | 1   |

|                                 | +   | -   | *   | d   |     |
| ------------------------------- | --- | --- | --- | --- | --- |
| A = {1, 2, 4, 6, 7, 8, 9}       | X   | X   |     | E   | 0   |
| X = {3, 8, 9}                   |     |     |     | E   | 0   |
| E = {9, 10, 11, 12, 17, 18, 19} |     |     | F   | E   | 1   |
| F = {13, 14}                    |     |     |     | G   | 0   |
| G = {14, 15, 16, 19}            |     |     |     | G   | 1   |

![[Pasted image 20241011152534.png]]

![[Pasted image 20241011152559.png]]

![[Pasted image 20241011152636.png]]

Pozicija je ponistiva ako je $*$, ako je | a jedna od dece je ponistiva ili ako je bilo koji cvor i oba deteta su ponistiva.

![[Pasted image 20241011152829.png]]

![[Pasted image 20241011152934.png]]


### Vezba

![[Pasted image 20241011153101.png]]

