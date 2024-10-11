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


### 