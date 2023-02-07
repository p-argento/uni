# Array
- gli array (sia statici sia dinamici) sono sempre passati per riferimento (o meglio puntatore) alle funzioni
	- quindi ogni modifica viene applicata anche all'array originario (salvo const)
	- un array statico viene implicitamente convertito a puntatore (infatti dimensione non è accessibile)
		- questo fenomento viene detto decadimento da array a puntatore (array to pointer decay)
-  infatti nel passare un vettore ad un funzione, questo decadrà a puntatore, perdendo l'informazione del sizeof
	- questo succede anche se il parametro viene dichiarato con le quadre (funziona, ma non è formalmente corretto)
- un array dinamico si gestisce utilizzando un puntatore a puntatore
	- si può usare la notazione con le quadre

# Funzioni const
- le funzioni membro const NON possono modificare l'oggetto a cui sono applicate
- sono importanti perchè ad ==oggetti classe costant==i possono essere applicate solo funzioni membro costanti
- l'attributo si aggiunge in fondo alla dichiarazione e va ripetuto nella definzione
	- `double reale() const;`


# Unsigned
- unsigned int = -3
	- compila? sì perchè avviene la conversione implicita, tuttavia prende la stringa di bit e la copia così com'è, indipendetemente dalla rappresentazione
	- quindi stamperà probabilmente con il c2
- unsigned int = 1u (oppure 1U)
	- è l'unico modo per non fare conversione iimplicita

per gli unsigned, oltre alle 4 operazioni aritmetiche, esistono anche 4 operazioni logiche bit a bit + traslazione a dx o sx

# Operazioni sui bit
settare un bit a 1
	```number |= 1u << n;```
		per settare l'ennesimo bit a 1 (zero-based)


# Lista di inizializzazione
DEVONO essere inizializzati
	- i membri dato const della classe
	- i membri dato reference della classe
	- i membri dato di tipo classe
> Si usano nella definizione e non nella dichiarazione

- Una lista di inizializzazione inizializza i membri della classe prima dell'esecuzione del corpo del costruttore.
- riguarda
	- oggetto -> deve essere un membro della classe.
	- argomento -> può essere uno dei parametri del costruttore, una chiamata di funzione o un altro oggetto


# Break e continue
- break esce dal loop
- continue salta una iterazione

# Conversioni
- Negli operatori binari, l'operando di lunghezza minore viene convertito in quello di lunghezza maggiore.
- conversioni significative
	- un enum può essere assegnato anche a int o double perchè è un numero

# Priorità operatori
Incremento postfisso
- `*p++` come default
	- prima incrementa, poi dereferenzia `*(p++)` 
	- quindi se è da solo non succede nulla, se non incrementare il puntatore +1
- `*p+1` come default
	- prima dereferenzia, poi incrementa `(*p)+1`
	- quindi il contrario del precedente
- `a[1]++` come default
	- prima dereferenzia e poi incrementa `(a[0])++`
	- effettivamente somiglia più a `*p+1` visto che `(*(a+1))++`
	- è chiaro quindi che l'operatore [] ha una priorità molto alta

# Proprietà operatori
Proprietà operatori
1. posizione (prefisso, postfisso, infisso)
2. arietà (numero di argomenti)
3. priorità (ordine di esecuzione)
4. associatività ( a destra o a sinistra)

# Priorità operatori
Vedi gruppi

# Funzioni
- nel caso di argomenti default, questi devono essere gli ultimi, ossia gli argomenti che saranno inclusi saranno considerati come primi
- puntatori a funzioni

# Unioni
- in momenti diversi può contenere dati di tipo diverso, ma comunque UN SOLO DATO per volta
	- riserva quindi spazio per il più grande tra quelli indicati
	- la sintassi è uguale a quella delle struct

# Algoritmi di ordinamento
- bubble sort
	- ogni volta parto dal fondo e porto fino al punto in cui deve stare

---
# Classi

## Assegnamento tra classi
- l'assegnamento tra classi effettua la ricopiatura membro a membro 
	- se non ridefinito diversamente)
	- se però si tratta di inizializzazione, invece, parte il costruttore di copia
	- <mark class="hltr-yellow">non esistono altre operazioni predefinite</mark>

## Visibilità a livello di classe
- l'operatore :: può essere usato solo per campi dato non statici
- nel caso di classe annidata
	- devono essere usati due operatori :: consecutivi
	- nessuna delle due classi ha diritto di accesso alla parte privata dell'altra

# Modularità
- la modifica di un file di intestazione richiede la ricompilazione di tutti i file che lo includono
	- il file di intestazione deve essere incluso in tutti i moduli che lo utilizzano
- la modifica di un file di realizzazione richiede la ricompilazione solo di quel file

## Funzioni globali
- non sono membro di alcuna classe
	- non possono quindi accedere alla parte privata della classe a meno di essere dichiarate friend dentro la classe stessa
	- non possono usare il puntatotore this
- quando ridefiniamo un operatore per una classe come funzione globale stiamo infatti
	- usando friend
	- facendo overloading di una funzione globale, con un parametro del tipo classe

## Costruttore
- viene invocato subito dopo che è stata riservata la memoria per i campi dati
- il costruttore default può essere implementato in due modi (alternativi)
	- 1. overloading
		- in base al numero di argomenti, partirà un costruttore diverso definito diversamente
	- 2. argomenti default
		- devono essere inseriti nella dichiarazione tra i parametri
		- permettono quindi di chiamare il costruttore con un numero minore di argomenti
		- invece nel caso di membri dato const (e array ?) si devono usare le liste di inizializzazione nella definizione
		-  si può usare questa scrittua soltanto se il costruttore può essere invocato anche con un elemento solo	  ![[Pasted image 20230129104755.png]]
- regole di chiamata
	- per oggetti automatici, con la definizione
	- per oggetti dinamici, con l'operatore new
	- per oggetti static, all'inizio del programma

## Distruttore
- è obbligatorio quando il costruttore alloca memoria dinamica
	- altrimenti l'oggetto allocato dinamicamente rimarrebbe dov'è
- regole di chiamata
	- per oggetti automatici, al termine del blocco in cui sono stati definiti
	- per oggetti dinamici, con l'operatore delete
	- per oggetti statici, al termine del programma
- gli oggetti con lo stesso tempo di vita vengono distrutti nell'ordine inverso a quello in cui sono definiti
	- ad esempio in un blocco, pensa allo stack

## Costruttori di copia
- il costruttore di copia predefinito effettua una ricopiatura membro a membro dei campi dati
- casi in cui viene applicato
	- 1. oggetto classe inizializzato con un altro oggetto della stessa classe
	- 2. oggetto classe passato per valore in una funzione
	- 3. oggetto classe restituito per valore
- deve essere ridefinito per le classi che prevedono memoria libera
	- altrimenti i puntatori punteranno allo stesso oggetto
	- quando viene distrutto l'oggetto, questo si distruggerà anche per la copia
- può essere nascosto dichiarandolo nell parte privata della funzione
	- in questo modo non si potranno passare per valore o restituire valori del tipo classe

## Array di oggetti classe
- costruttore e distruttore vengono richiamati per ogni elemento dell'array
- se gli elementi non sono tutti inizializzati, è importante avere un costruttore default


---
# Ripasso flash orale
- SIGSEV
	- errore a tempo di compilazione, se si sta cercando di accedere ad un'area di memoria  riservata oppure inesistente, solitamente attraverso puntatori
- Strcpy()
	- anche se sforiamo il vettore precedentemente allocato, stampa sempre correttamente e lo strlen sarà quello della stringa sorgente
- tipi
	- tipi predefiniti sono 5
		- int, unsigned, float, double, char
	- tipi derivati sono 6
		- array, pointer, reference, struct, union, class
- literal
	- sono tutti quei valori inseriti dal programmatore, ad esempio in int a = 5 il literal è 5, rappresentano quindi il valore assegnato agli oggetti
- linker
	- combina tutti i file dell'unità di compilazione per generare un unico eseguibile, seguendo le direttive del preprocessore, in particolare gli \#include
- proprietà degli algoritmi
	- corretti
	- non ambigui
	- efficienti
	- eseguibili in tempo finito
- approccio compilato vs interpretato
	- compilato, viene compilato, ossia tradotto nel linguaggio macchina del calcolatore specifico e non è quindi cross-platform. Esempi sono C e C++, che sono particolarmente efficienti
	- interpretato, esiste un interprete che lavora riga per riga ed  è quindi più lento, ma cross-platform. Esempi sono Javascript, Python, php.
- tipi di operazioni
	- sequenziali, ossia singole azioni che terminano subito
	- condizionali
	- iterative
- funzioni ricorsive
	- necessità di
		- un caso base (per terminare il programma)
		- un passo ricorsivo (che richiama la funzione)
- le operazioni di bit sono molto leggere, quindi un buon compilatore dovrebbe utilizzarle spesso
	- non ciclano, ossia se si va oltre lo spazio destinato dal tipo, i bit vanno persi
	- è implicito l'operatore resto per ottenere i valori che realmente spostano i bit
- sintassi
	- si riferisce alle regole con cui bisogna scrivere nel linguaggio
	- invece la semantica si riferisce al significato
- programmazione a moduli
	- consiste in
		- modulo server (servitore) include compito.cpp e compito.h
		- modulo client (cliente) che richiama le funzioni definite
	- vantaggi
		- information hiding, ossia mascherare l'implementazione di una classe
		- successive modifiche solo lato server
		- prestazioni migliori, in quanto basta ricompilare solo alcuni file in caso di modifiche
- overloading funzioni
	- !!! non possono differire soltanto per il return type
	- !!! nel valutare a quale funzione fare riferimento, prima controlla il numero di argomenti richiamati, poi il tipo (effettuando meno conversioni implicite possibili)
- overloading operatori
	- NON si posso ridefinire :: . .*
	- per gli operatori binari è preferibile dichiarare la funzione friend
	- l'operator= è l'unico predefinito nel caso dell classi
- incremento prefisso e postfisso
	- l'incremento prefisso ++a restituisce un left value (e ha associatività a sx)
		- quindi è concatenabile (++++a) funziona
	- l'incremento postfisso a++ restituisce un right value (e ha associatività a dx)
		- quindi non è concatenabile, perchè ha restituito il valore di a prima dell'incremento, che ormai non è più una variabile assegnabile in memoria
- differenza tra left value e right value
	- ai left value è possibile assegnare un valore, infatti HA UN INDIRIZZO IN MEMORIA
	- invece ai right value no, in quanto non esistono in memoria, ad esempio a = 3+2;
- cortocircuito
	- meccanismo relativo agli operatori binari, per cui se il primo operatore è falso, allora il secondo non verrà nemmeno valutato
- preprocessore
	- define, permette di definire delle macro, ossia espressioni che verranno sostituite alle parole dal preprocessore, ad esempio
		- \#define scambia(a,b) int temp=a;a=b;b=temp;
		- \#define C 3; // per un valore costante
	- può essere usata in combinazione con la compilazione condizionale
		- if (o ifdef o ifndef), elif, else, endif

---
# STREAM

## ISTREAM
- preleva dallo stream e trasforma in caratteri
	- i caratteri entrano a far parte di cin soltanto dopo aver premuto il tasto di ritorno carrello
	- in pratica, se lo spazio puntato è bianco, si passa alla casella successiva fino ad incontrarne uno *coerente con la sintassi richiesta*, continuando fintanto che la sintassi rimane corretta, altrimenti si ferma
	- per prelevare anche gli spazi bianchi si usa la funzione membro della classe istream `cin.get(nome var da assegnare)` invece dell'overloading dell'operator<<
	- poichè l'operator<< è associativo a sinistra, si possono concatenare le letture
- si può usare `cin >> n`  come condizione di un if o un loop
	- chiederà l'ingresso ogni volta
	- sarà vera se la condizione del cin è rispettata, ossia se il valore inserito corrisponde a quello indicato dalla variabile (sintassi corretta)
	- se però lo stream va in stato di errore, è necessario un ripristino tramite `cin.clear`
		- se un programma si aspetta la marca di fine stream, questa va inserita con control + D (nei sistemi unix)

- l'oggetto cin è un'istanza predefinita della classe istreamù
- la funzione chiave è get() che preleva un carattere e lo restituisce convertito in intero
- lo stato è una configurazione di bit
	- 

## OSTREAM
- converte lo stream in una sequenza di caratteri
- la funzione membro della classe ostream put() è quella chiave,
	- trasferisce il carattere sullo stream di uscita
	- in realtà è un pezzo della funzione write() che trasferisce una sequenza di n caratteri sullo stream di uscita
- bool ed enum vengono implicitamente convertiti in int (codifica del valore)
- la ridefinizione tramite overloading degli operatori di lettura e scrittura DEVE avvenire tramite funzioni globali
- cout e cerr sono istanze predefinite
- manipolatori della classe ostream
	- endl (inserisce \n e svuota il buffer)
	- dec, hex, oct
	- boolalpha (inserisce bool come true e false invece di 1 e 0)

## FSTREAM
- per usare gli stream di file, bisogna includere \<fstream\>
- diverse implementazioni della funzione open() dipendono dalla costante indicate
	- lettura.open("file1.in", ios::in)
		- (alternativa `ifstream lettura("file.txt")`, senza dover quindi specificare la costante)
		- il file deve esistere
	- scrittura.open("file.out", ios::out)
		- (alternativa `ofstream scrittura("file.txt")`)
		- se il file non esiste, viene creato
		- in ogni caso viene cancellato il contenuto precedente
	- aggiunta.open("file.txt", ios::out|ios::app)
		- alternativa `ofstream scrittura("file.txt", ios::app)`
		- se non esiste, viene creato
		- il puntatore si sposta in corrispondenza della marca finale di fine stream
- con uno stream aperto, si possono usare gli overloading degli operatori come con istream e ostream
	- lettura >> x
	- scrittura << 10
- per chiudere uno stream si usa (si chiudono comunque alla fine del programma)
	- lettura.close()
	- scrittura.close()
- possono essere riaperti e associati ad altri file

## IOMANIP
- libreria che contiene manipolatori per il controllo del formato
- sono
	- setw(int)
		- stabilisce un numero minimo di caratteri per la stampa
		- è valido soltanto per l'istruzione successiva (gli altri invece rimangono a oltranza)
	- setfill(char)
		- stabilisce quale carattere utilizzare per riempire lo spazio vuota precedente definito da setw() (default spazio bianco)
		- `cout << setfill('0') << setw(10) << d << endl;`
			- >> `000000.016`
	- setprecision(int)
		- numero di cifre significative per la stampa di reali (escludendo gli zeri ovviamente)

## STATO DI UNO STREAM
- lo stato di uno stream è una configurazione di bit, detti bit di stato
	- lo stato è corretto (good) se tutti i bit di stato valgono 0
	- viene restituito il complemento della funzione fail()
- i 3 bit che definiscono lo stato sono
	- fail (posto ad 1 se errore recuperabile)
	- bad (posto a 1 se errore non recuperabile)
	- eof (posto a 1 se legge marca di fine stream)
- le funzioni che possono essere utilizzate per scoprire il valore di questi bit sono (ad esempio `istanzastream.fail()`)
	- fail() (ritorna valore del bit fail)
	- bad() (ritorna valore del bit bad)
	- eof() (ritorna valore del bit eof)
- inoltre ci sono altre due funzioni
	- good() restituisce true se tutti i 3 bit sono a 0
	- clear() ha per argomento uno tra i seguenti enum per stabilire il nuovo valore dello stato
		- ios::failbit (pone a 1 bit fail)
		- ios::badbit (pone a 1 bit bad)(e quindi anche bit fail)
		- ios::eofbit (pone a 1 bit eof)