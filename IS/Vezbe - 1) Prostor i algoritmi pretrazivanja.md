### DFS - Depth First Search
Mehanizam algoritma je da krecemo od pocetnog cvora i na stek upisujemo svu njegovu decu. Sa vrha steka uzimamo jedno dete i dodajemo svu njegovu decu. Ovaj postupak se ponavlja sve dok ne dodjemo do ciljanog cvora. 

Ovaj postupak ne daje najbolje performanse ali je koristan i jednostavan za implementaciju ako nam performanse nisu bitne.

### BFS - Breadth First Search
Mehanizam i slican kao god DFS samo sto se ne koristi stek vec se koristi red. Znaci novi elementi idu na kraj reda a uzima se onaj koji je najdavnije dodat u red.

Ni ovaj postupak ne garantuje optimalno resenje, osim ako u pitanju nije da cena svake grane bude ista. U tom slucaju ovaj algoritam daje optimalan rezultat.

### BF - Best First
Algoritam za ovaj postupak je sledeci: dodati decu izabranog cvora u red, sortirati red na osnovu heuristike rastuce, i zatim uzeti prvi element iz liste posto on ima najmanju heuristiku. Ovim postupkmon se sigurno nalazi resenje iskljucivo na osnovu heuristike cvorova.

Heuristika su neki dodatni podaci koje mozemo da iskoristimo da bi dosli do resenje, medjutim ovo ne daje optimalno resenje.

### BBS - Branch and Bound Search
Mehanizam je sledeci: na pocetku cena startnog cvora je 0, svaki sledeci cvor sledbenik se upisuje u listu i na njemu se dodaje cena njegovog roditelja plus cena kojom kosta da se dodje do tog cvora. Zatim se lista sortira rastuce i uzima se najevtini ruta.

Na ovaj nacin mozemo naci optimalno resenje cak mozemo da implementiramo i DP u ovaj algoritam tako sto ako nadjemo putanju do nekog cvora koja je optimalnija od predhodno nadjene putanje mozemo tu skuplu putanju kompletno da izbacimo iz liste posto je neefikasna i ubrzavamo time algoritam.

### $A^*$ - A star

Ovaj algoritam funkcioniste slicno kao BBS samo sto pored cene gleda i heuristiku tako sto gledamo zbirnu vrednost cene putanje zajedno sa heuristikom i onda bira putanju sa najmanjom vrednoscu. 

Ovaj algoritam garantuje optimalno resenje samo ako heuristika potcenjuje cenu resenja.

### ID $A^*$ - Iterative deepening $A^*$

Uzeti kumulativnu vrednost cene i heuristike. Taj broj postaje prag preko koga ne sme da se predje. uzeti sve povezane cvorove i ako njihova kumulativna vrednost je veca od praga ti cvorovi se odbacuju. Od preostalih cvorova uzeti onaj sa najmanjom kumulativnom vrednoscu i ici dalje. Ako dodjemo u situaciju da nema vise cvorova a nismo dosli do resenja prag povecavamo na najmanju kumulativnu vrednost do tada odbacenih cvorova i krecemo od pocetka.

ID A* garantuje pronalaženje optimalne putanje ukoliko heuristika potcenjuje cenu rešenja.

Algoritam ID A* zahteva manje memorije jer čuva samo jednu putanju od korena do čvora koji se trenutno razmatra, dok algoritam A* zahteva više memorije jer u memoriji čuva sve parcijalne putanje koje trenutno razmatra.

Algoritam ID A* često obilazi iste čvorove više puta, dok algoritam A* razmatra sve otvorene parcijalne putanje te ga dobra heuristika može voditi do rešenja u značajno manjem vremenu.

### Heuristika table

Ako imamo tablu punu kvadrata i zelimo da najdemo heuristiku onda je najbolje sledeci postupak. 

![[Pasted image 20241011161116.png]]

Posmatramo zamak koji je okruzen crvenom bojom i zelimo da nadjemo najkraci put do drugih sela. Ako ignorisemo puteve i samo gledamo hvadrate i njihovu direktnu putanju do sela mozemo naci najoptimalniju putanju i te brojeve mozemo uzeti kao heuristiku.

![[Pasted image 20241011161236.png]]
### Zadaci za vezbu

![[Pasted image 20241011155340.png]]

![[Pasted image 20241011155407.png]]

![[Pasted image 20241011155421.png]]

![[Pasted image 20241011155436.png]]

