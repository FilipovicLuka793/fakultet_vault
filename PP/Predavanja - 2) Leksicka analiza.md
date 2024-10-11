### Konacni automati

![[Pasted image 20241005104637.png]]

![[Pasted image 20241005104704.png]]
Ovakav automat gde je ulaz i stanje jednoznacno naziva se <span style="color:rgb(255, 0, 0)">Deterministicki konacni automat </span>(DKA)

### Nedeterministicki konacni automati

![[Pasted image 20241007143455.png]]

- S0 ima prelaz za $\epsilon$ 
- S1 ima dva razlicita prelaza za a

Zbog ovih karakteristika u pitanju je <span style="color:rgb(255, 0, 0)">nedeterministicki konacni automat (NKA)</span> 

Generalno, NKA prihvata ulaznu sekvencu x ako i samo za x postoji scenario promene stanja iz nekog od starthinh stanja do nekog od stanja prihvacanja.

![[Pasted image 20241007144219.png]]

### Regularni izrazi

Regularni izraz opisuje tacno isti skup jezika kao konacni automat:
- Za scaki regularni izraz moze se naci konacni automat koji opisuje jezik kao taj izraz
- Za svaki konacni automat moze se naci regularni izraz koji opisuje isti jezik kao taj automat

$$
\large
\begin{split}
L(abc) = {abc} \\
L(a | b | c) = {a, b, c} \\
L[(a | b)(c | d)] = {ac, ad, bc, bd} \\
L(a^*) = {\epsilon, a, aa, aaa, \dots} \\
L[(a | b)^+] = {a, b, aa, ab, ba, bb, aaa, aab, aba, \dots} \\
\end{split}
$$

### Konstrukcija konacnog automata iz regularnog izraza

<font color="#ff0000">Bitni automati, zapamtiti napamet!!!</font>

![[Pasted image 20241007151718.png]] 

![[Pasted image 20241007151839.png]]

![[Pasted image 20241007151936.png]]

