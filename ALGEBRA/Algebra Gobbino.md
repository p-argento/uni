# LEZ 11
- gruppo
- gruppo commutativo
- anello
- corpo
- campo
- modulo
- spazio vettoriale

## campo
è un insieme K sul quale sono definite 2 operazioni binarie (ossia somma e prodotto con 2 input e 1 output)

Ci sono 4 proprietà per la somma e 4 per il prodotto.
Poi c'è la distributiva per mettere in relazione somma e prodotto.

Esempi di campo sono R, Q e C.
Non sono campi invece N, Z e R[x] ossia l'insieme dei polinomi 

## spazio vettoriale
sia K un campo (di solito R), uno spazio vettoriale V è un insieme più due operazioni
- somma
- prodotto per scalare

Ci sono 4 proprietà della somma (che sono poi le stesse di prima ma con i vettori).
Ci sono 4 proprietà del prodotto per scalare (che sono diverse da prima).

Poi c'è la distributiva per metterli in relazione.

Esempi di spazio vettoriale. (con K = R).
1. V = R
2. V = R
3. l'insieme delle matrici M mxn è uno spazio vettoriale
	1. 0 è la matrice nulla
	2. le operazioni sono la somma di matrici e il prodotto di una matrice per un numero (non consideriamo il prodotto tra matrici)
4. l'insieme dei polinomi è uno spazio vettoriale rispetto alle operazioni
	1. somma di 2 polinomi
	2. prodotto di un polinomio per un numero
5. R <= 3 [x] sono i polinomi a coeff reali di grado <= 3
	1. è uno spazio vettoriale rispetto alle operazioni dette sopra
6. R >= 3 [x] NON è uno spazio vettoriale perchè in una somma si potrebbero cancellare i termini di grado 3 e quindi non sarebbe più nell'insieme

## Sottospazi vettoriali
---
Sia V uno spazio vettoriale.
Un sottospazio vettoriale è un sottoinsieme W contenuto in V che è chiuso rispetto alla somma e rispetto al prodotto per uno scalare.

Osservazione.
SI può verificare che W è a sua volta uno spazio vettoriale, con le operazioni che eredita da V.

Esempi.

Come dimostro che un certo W NON è un certo sottospazio vettoriale? Basta fare una di queste cose. Basta trovare due elementi la cui somma non sta in W.

E dimostrare che È un sottospazio vettoriale?
 

# Lez 12
Introduciamo
- vettori linearmente dipendenti e indipendenti
- SPAN
- generatori
- basi
- dimensione
- combinazioni lineari

## Combinazione lineare
Vuo dire prendere un certo numero di vettori, moltiplicarli per dei numeri e sommarli

## SPAN
Insieme di tutte le possibili combinazioni lineari di $$v_1,...,v_n$$ciò che varia sono i numeri che metto davanti.

Lo span di un singolo vettore è l'insieme dei multipli di quel vettore, ossia la retta con direzione data dal vettore.

Esempio.
Se prendiamo due vettori v e w in R3 allora 

Proprietà.
Lo span è un sottospazio vettoriale di V?
Devo dimostrare che
1. la somma di due combinazioni lineari sia ancora una combinazione lineare.
2. il prodotto per scalare è ancora una comb lineare.

## Generatori
I vettori sono generatori se il loro span = V
Ossia se ogni vettore v dello spazio si può scrivere come combinazione lineare dei vettori generatori, ossia se esistono coefficienti tali per cui 

Come verificarlo?
Prendo un qualunque 

## Linearmente indipendenti
Se l'unica combinazione lineare che viene 0 dei vettori è quella con i coefficienti nulli.
Altrimenti si dicono linearmente dipendenti.

Se non si vede a occhio, si scrive av1+bv2+cv3 = (0,0,0)
Poi risolvevo il sistema e vedevo se c'erano soluzioni diverse da a=b=c=0;

## Base
Un sottoinsieme di V si dice Base di V se
1. v1,..., vn sono linearmente indipendenti
2. v1,...,vn sono generatori di v

Base canonica.
Se ha 1 in un posto e 0 negli altri. Ad esempio (1,0,0),(0,1,0),(0,0,1) è una base di R3.

Certe volte conviene usare una base strana al posto di quella canonica.

Teorema fondamentale delle basi.
Ogni vettore v si scrive in MODO UNICO come combinazione lineare di v1,..,vn

Esempio.
Una base sono i mattoncini di cui è formato lo spazio.
Data la base, un polinomio può essere pensato come vettore, in cui ci sono i coefficienti dell'unica combinazione lineare che descrive il polinomio dato.

---






