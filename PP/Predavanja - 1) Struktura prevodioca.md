Prevodioc se deli u:
1. Lekser
2. Parser
3. Semanticka analiza
4. Optimizacija
5. Generisanje koda

Obicno su danas programski prevodioci napisani da budu dvoprolazni. Prvi prolaz je frontend deo gde se prevodi kod sa C, C++, Java, Python ili nekog drugog programskog jezika na medjukod, taj medjukod se zatim optimizuje da efikasnije radi, a tek onda ide u backend deo koji pretvara taj medjukod u asemblerski kod za razliciti hrader.

![[Pasted image 20241004144658.png]]

Ovaj pristup je jako dobar posto garantuje da bez obszira na koji jezik koristimo frontend deo ce uvek uzbaciti medjukod koji backend deo moze da protumaci i da prevede za razlicite hardvere.