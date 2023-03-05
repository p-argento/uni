o2023-03-03
# Template
## Classi modello
Possiamo definire classi come classi modello.

# Gerarchia delle classi
Posso dichiarare classi padre.
I figli ereditano i metodi dai padri, ma posso aggiungerne altri.
Ereditano tutto. Sia campi pubblici che privati. Sia campi dati sia metodi.
Questo dovrebbe facilitare manutenzione e correzione di errori.

Principio di programmazione a oggetti.
Prima di estendere un programma, bisogno tenere presente il diagramma delle classi.
Estendere non significa quindi modificare il precedente, ma aggiungere. Anche perchè spesso non si ha il codice sorgente.

Come fare?
```c++
class studente : public persona{
public:
	int esami;
	int matricola;
}

class impiegato : public persona{

}
```
La classe derivata studente deriva dalla classe persona.
Ogni oggetto di tipo studente ci sarà in memoria una parte derivata dalla classe persona e una nuova.
Impiegato è un *fratello* di studente.

Che cosa succede con gli oggetti di varie classi derivate?
Se assegno un oggetto di tipo persona a un borsista?
Il *supertipo* sarebbe il padre (o il nonno).
> Un oggetto (puntatore ad oggetto) di un tipo può essere convertito in un supertipo (puntatore ad un supertipo), ma non vale veceversa

Compatibilità tra tipi.
Posso assegnare un sottotipo ad un supertipo (conversione implicita).
Ma non viceversa, ossia un supertipo ad un sottotipo.
Nemmeno un'assegnazione tra fratelli, in quanto tipi diversi.

Compatibilità tra puntatori.
Attenzione alla conversione implicita che non cancella campi, ma semplicemente si limita ad accedere ad alcuni campi escludendone altri.

Regole di visibilità.
```c++
b->studente::esami = 5 // per accedere al campo dato esami di studente
```







