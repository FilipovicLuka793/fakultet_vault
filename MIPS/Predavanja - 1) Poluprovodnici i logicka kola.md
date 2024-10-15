## Omov zakon

$$
\large
\begin{flalign*}
&U = R * I \\
&R - \text{otpornost kroz koju tece struja} \\
&I - \text{struja koja protice kroz otpornik} \\
&U - \text{pad napona na otpornosti R usled proticanja struje I}
\end{flalign*}
$$
![[Pasted image 20241007161253.png]]

## Poluprovodnici

Postoje 2 vrste: P tip i N tip.

Ovi tipovi odredjuju u kom temperaturnom opsegu cip moze da radi.

Kombinovanjem poluprovodnika moze se dobiti:
- Dioda
- Bipolarni tranzistor
- MOS tranzistor
- Ostalo

### Dioda

![[Pasted image 20241007162105.png]]

Dioda nece da propusta struju pod malim naponom vec mora da prodje odredjena kolicina struje da bi struja prosla, i to samo sa leva na desno. Kada pokusamo da pustimo struju sa plusa ka minus dioda nece dozvoliti da struja prodje.

Pod uslovom da je dioda direktno polarisana sa $U = 0.7 V$, dioda se ponasa kao idealni naponski generator. Ako je napon ispod ovog praga, znaci $0\leq U<0.7V$, onda se dioda tretira kao otvorena veza.

Diodu nikada ne treba povezivati direktno na napajanje, obavezno staviti izmedju njih neki otpornik.

![[Pasted image 20241007191820.png]]

### Bipolarni tranzistor

Postoje dve vrste: PNP i NPN. 

NPN ima bolje karakteristike i cesce se koristi.

Moze da radi u vise rezima:
- Zakocen
- Zasicen
- Ostali rezimi

Koristi se kao prekidac:
- Zakocen - otvoren prekidac
- Zasicen - zatvoren prekidac sa konstantnim padom napona $V_{CES}$ 

B - baza
 - kontrolni ulaz
 - racuna se napon prema emiteru

E - emiter
- Vezuje se na GND (NPN)
- Vezuje se na $V_{CC}$  (PNP)

C - kolektor
- Vezuje se za potrosac

![[Pasted image 20241007204048.png]]


### Kola sa otvorenim kolktorom

![[Pasted image 20241012163217.png]]

Ta otvoreno veza nam utcari obezbedjuje da izlaz bude u stanje visoke ipedanse da ne bi pregorele zice ako su povezane.

![[Pasted image 20241012163524.png]]

### Smitovo kolo

![[Pasted image 20241012164151.png]]

![[Pasted image 20241012164204.png]]

Radi po principu kada dostigne jedinicu i potencijal pocne da pada vrednost jedan ostaje sve dok ne dodje do donje granici gde tek onda postaje 0. Isto i suprotno ako potencijal krene da raste i prodje gornju granicu ne postaje odmah 1 ili neka nedefinisana vrednost vec ostaje na 0 sve dok ne dodje do gornje granice i tada postaje 1.

### MOS tranzistor

![[Pasted image 20241012171808.png]]

Koristi se kao prekidac.

NMOS - kada je 1 onda provodi, kada je 0 koci
PMOS - kada je 1 onda koci, kada je 0 provodi

![[Pasted image 20241012171931.png]]

![[Pasted image 20241012172340.png]]


## Logicka kola

![[Pasted image 20241013005244.png]]

Ovo je sekvencijalno logicko kolo odnosno Lec. 

Lecevi garantuju da ako je R bio postavljen na 1 i u nekom trenutku se postavi na 0 vrednost Q ce idalje biti 0. Bolje receno ovo kolo obezbedjuju da vrednosti Q i ne-Q ostanu iste. Ali je jako bitno da nikada se ne postavi R i S na 1 u isto vreme posto onda kolo nece dobro funkcionisati.