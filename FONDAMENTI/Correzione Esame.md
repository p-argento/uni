1. il prezzo si doveva modificare nel carrello?
2. nel distruttore, se un carrello è uscito e dealloco un nullptr che succede?


---
Correzioni effettive
1.  crea_prodotto
	1. controllo p<=0
	2. strlen+1
2. esponi
	1. typo qu<0 invece di pu=0 nel controllo iniziale
	2.  questione aggiornamento prezzo
	3. typo += quanti
3. esponi (overloading)
	1. controllo quantità
4. metti_nel_carrello
	1. (questione prodotto già presente)
		1. 
	2. typo += quantita (gestione quantita)
	3. manca aggiornamento prezzo
5. ostream
	1. spazio dopo ultimo elemento carrello

1. spazio prima dell'elemento e non dopo
2.  strlen +1 nella metti carrello
3. 