## Java Basics



### Class Structure

**- Fields & Method**  

Ogni classe java è composta da due elementi primari:

\- metodi (methods)

\- campi (detti anche variabili o attributi) (fields, variables)

entrambi questi elementi vengo anche definiti come membri di una classe (members)



In java vengono utilizzate delle keywords, parole con un significato speciale che sono riservate.

Chap 1 - Java Building Blocks

**Definizione di classe**:



*public class Animal{*

*}*



*[{\**access modifier**}] [**class**] [class name]*



**Definizione di variabili:**



*String name;*



*[{\**access modifier**}] [type] [identifier] { = initialChap 1 - Java Building Blocksization}*



**Definizione di metodo:**

**Chap 1 - Java Building Blocks**

public int numberVisitors(int month)



*[{\**access modifier**}] [return type] [method name] ( {[parameter type] [parameter name], ...} )*



La definizione di un metodo viene anche detta 'firma del metodo' (method signature).

Il return type di un metodo, può essere un tipo primitivo, una classe oppure 'void' (keyword), nel caso sia void il metodo non restituisce alcun valore.



NOTA: gli *access modifier* sono opzionali sia nella definizione di una variabile sia di un metodo, se non presenti viene usato un *access modifier* di default.



**- Comments**



In java esistono 3 tipologie di commenti:



- single line comment:
  // single line comment
  per ogni singola riga tutto il testo che si trova dopo i caratteri \\ viene ignorato dal compilatore
- multiple line comment:
  /*
   \* multiple line comment
   */ 
  Tutto il testo che si trova all'interno dei caratteri /* e */ viene ignorato dal compilatore
- javadocs comment
  /**
   \* @Autohor Davide Gulli
   */
  Non utile ai fini dell'esame e non presente nelle specifiche del linguaggio



Esempi di commenti validi:



- // /* valid comment */
- // // valid comment
- //// valid comment
- /* //valid comment */



Esempi di commenti non validi:



- /* /* non-valid comment */ */

​     

**- Classes vs Files**



Nella maggior parte dei casi una classe corrisponde ad un file .java, avente lo stesso nome della classe, normalmente la classe è pubblica, ma in java è possibile anche avere la definizione di più classi all'interno dello stesso file, in questo caso una sola classe può essere pubblica ed il nome del file .java deve corrispondere al nome della classe pubblica.



**Regole:**

- Se in un file .java ho una classe *public*, il nome del file deve corrispondere al nome della classe
- Se in un file .java non sono presenti classi *public*, non è necessaria la corrispondenza del nome del file con quello della classe
- In un file .java è possibile definire quante classi si vuole, ma solamente una potrà essere *public*, solo in questa maniera sarà rispettata la corrispondenza tra il nome della classe pubblica e quello del file
- In fase di compilazione per ogni classe presente all'interno di un file .java viene creato un file .class avente il nome della singola classe
- In un file non possono essere definite due classi con lo stesso nome
- Non è possibile definire una classe *private* o *protected*, il modificatore di accesso non è ammesso per le classi "non inner"
- E' possibile eseguire il metodo main di una classe che non é *public*



**- Main Method**



Il metodo *main* è il punto di start del proprio programma java, senza il quale un programma non può essere eseguito.



*public static void main(String args[]){...}*



- Il metodo main deve essere *public*  e *static* altrimenti la jvm non sarà in grado di invocare il metodo e quando si proverà a lanciare il programma verrà sollevato un errore

- Il metodo

   

  main

   

  prevede un paramentro di tipo array di stringhe che può essere definito in uno qualsiasi dei seguenti modi:

  - String[] args
  - String args[]
  - String... args

- Inoltre l'identificativo del parametro può essere scelto dal programmatore 



\- Compilazione e Lancio di un programma



Un programma per essere lanciato deve essere prima di tutto compilato:



​     *javac Main.java*



dopo il comando *javac* deve seguire il nome del file completo compresa l'estensione .java

Mentre per eseguire un programma:



​     *java Main*



dopo il comando *java* deve seguire il nome della classe java che contiene il metodo *main.* In questo caso non è necessario inserire l'estensione del file in quanto si fa riferimento al nome della classe, a conferma di questo si può verificare come sia possibile lanciare una classe con modificatore di accesso default che contenga un metodo *main,* dove il nome del file .java ed il nome della classe non corrispondono.



Quando si lancia l'esecuzione di un programma è possibile passare dei parametri



​     *java Main hello world first program*



ogni parola che segue il nome della classe è un parametro diverso,  lo spazio sancisce l'inizio di un nuovo parametro, se ho necessità di passare delle frasi con al loro interno dei spazzi potrò usare il carattere " per racchiudere la stringa



​     *java Main "hello world" "first program"*



ogni parametro viene trattato come una stringa (java.lang.String), non importa se sia un numero o un booleano.

Se nel codice si cerca di recuperare un parametro che non è stato passato verrà sollevata l'eccezione java.lang.ArrayIndexOutOfBuondsException 



Con un opzione del comando *java* è possibile indicare la posizione di classi esterne al programma ma usate all'interno di esso, ovvero importare jar e classi all'interno del classpath.



on windons:

​     *java -cp ".;C:\temp\someOtherLocation;c:/temp/myJar.jar" package.Main*



on unix:

​     *java -cp ".:C:\temp\someOtherLocation:c:/temp/myJar.jar" package.Main*



il carattere . è utilizzato per indicare di includere anche tutte le classi presenti nella posizione corrente, mentre i caratteri ; e : sono usati come separatori delle diverse posizioni dei file da includere, inoltre è possibile usare il carattere * per includere tutti i file .jar presenti all'interno di una singola directory.



**- Packages**



I packages sono una serie di identificativi separati da punti. Gli identificati seguono le stesse regole delle variabili possono contenere caratteri alfabetici, numeri, $, _ e non possono iniziare con un numero.



**- Wildcards**



Per selezionare più classi usando un solo import si usa il carattere *, questo seleziona solamente classi, quindi non seleziona i package figli, classi o metodi, può essere posizionato solamente al termine di un import.



**- Redundant Imports**



\- In ogni classe java di default viene importato il package java.lang.*, quindi è ridondante inserire l'import di questo package

\- Una classe java di default 'vede' le classi che si trovano nel suo stesso package, quindi non c'è necessità di importarle



**- Naming Conflicts**



Si possono verificare dei casi di conflitto nell'importazione di classi che hanno lo stesso nome, ad esempio:



​     *java.util.Date*

​     *java.sql.Date*



- importando due interi packages, usando la wildcards, che contengono delle classi che hanno lo stesso nome, usando una delle due classi nel programma si otterrà un errore di compilazione, in quanto il compilatore non è in grado di capire quale sia la classe da usare. Le possibili soluzioni sono le seguenti:
  - *java.util.Datejava.util.\**Il compilatore in caso di ambiguità da precedenza agli import espliciti, subordinando gli import che usano wildcard
  - usando la classe con il suo nome completamente qualificato, all'interno del programma: *java.util.Date*
- Non è possibile fare import espliciti di più classi che hanno lo stesso nome, in questo caso il compilatore darà subito un errore



**- Creating New Package**



Le classi che non presentano la definizione di un *package* risiedono all'interno del *default* package. I nomi dei *package* devono rispecchiare la struttura delle cartelle di file system all'interno delle quali si trovano.



**- Objects**



**- Constructors**



**\*new*** *class-type*();



*new Random();*



- I costruttori di un oggetto vengono chiamati al momento della creazione dell'oggetto, si presentano come metodi ma hanno lo stesso nome della classe e non hanno un return type.
- Se non viene definito un costruttore per la classe il compilatore ne fornisce uno di default che non fa nulla
- Nei test di esame potrebbe esserci dei metodi che sembrano costruttori, per creare difficoltà al candidato:
  *public void Random(){....}*nell'esempio precedente si noti la presenza di un return type, quindi non si tratta di un costruttore
- Esistono dei casi in cui si è obbligati a definire un costruttore (capitolo 5)
- I costruttori possono avere come access modifier: *public, default, proteced, private* seguono le regole classiche 
- In fase di inizializzazione di un oggetto il costruttore viene richiamato dopo l'instance initializer



**- Instance Initializer Blocks**



In java tutto ciò che si trova all'interno dei simboli { } è definito come code block.

I code blocks che si trovano al di fuori di un metodo si chiamano instance initializer, e vengono chiamati al momento dell'inizializzazione dell'oggetto.



- In fase di inizializzazione di un oggetto l'instance initializer viene richiamato prima dei costruttori
- All'interno di un initializer block non è possibile far riferimento ad un field che è definito successivamente all'initializer block
  *{name = "test";} //do not compileString name;*
- In un *initializer* non è possibile fare il throw di un eccezzione, altrimenti il compilatore solleverà un errore: initializer must be able to complete normally



**- Order of Initialization**



1. fields e initilizer block vengono eseguiti nell'ordine in cui sono stati definiti
2. i costruttori vengo eseguiti solamente dopo che sono stati inizializzati i fields e gli initializer blocks



**- Objects References vs Primitives**



**- Primitives**



In java esistono 8 tipi primitivi:





| boolean | 1 bit   | true, false |
| ------- | ------- | ----------- |
| byte    | 8 bits  | -128, +127  |
| short   | 16 bits | 123         |
| int     | 32 bits | 123         |
| long    | 64 bits | 123         |
| float   | 32 bits | 123.23F     |
| double  | 64 bits | 123.1234    |
| char    | 16 bits | 'a'         |



- quando nel codice si trova un valore numerico questo viene detto literal ad esempio:
  *int x = 123;*
  il compilatore di default assume che il valore sia un int, quindi i valori più piccoli di un int vengono promossi, ma si possono avere problemi con i valori che superano le dimensioni massime di int, ad esempio:
  *long y = 323456789; // does not compile*in questo caso è necessario indicare al compilatore che il literal non è un intero ma un long, e possibile farlo aggiungendo il carattere 'l' o 'L' alla fine del literal, ad esempio:
  *long y = 323456789L; // compile*

- se il valore literal è un floating-point, contiene la virgola, il compilatore di default assume che si tratti di un double, per avere un valore literal di tipo float è necessario aggiungere alla fine del literal il carattere "f" o "F", ad esempio:
  *float x = 123.23; // does not compile*il compilatore da un errore in fase di compilazione in quanto si cerca di inizializzare una variabile con dimensione di 32bits con un literal di dimensione di 64bits, senza effettuare il casting. L'inizializzazione corretta di una variabile di tipo float è la seguente:
  *float x = 123.22F; // compile*

- I literal possono essere espressi su basi differenti:

  - decimal: 56

  - octal: 023 - può contenere solamente i numeri da 0 a 7

  - hex: 0xFF - può contenere solamente i numeri da 0 a 9 ed i caratteri da A a F, il carattere x può essere sia maiuscolo che minuscolo, come anche i caratteri che compongono il literal

  - binary: 0b11 - può contenere solamente i numeri 0 e 1, il carattere b può essere sia maiuscolo che minuscolo

- I literal numerici possono contenere il carattere _ per facilitarne la lettura ad esempio:

  int oneMilion = 1_000_000; // compile

  - le uniche regole sintattiche sono che il carattere underscore non può trovarsi
    - all'inizio o alla fine di un literal:
      *int oneMilion = _1_000_000; // does not compile**int oneMilion = 1_000_000_; // does not compile*
    - prima o dopo il carattere . 
      *double x = 1000_.23 // does not compile**double x = 1000._23 // does not compile*



**- Reference Types**







**- Key differences**



- su una variabile di tipo reference non è null posso invocare dei metodi, i tipi primitivi non hanno metodi
- ad una variabile di tipo reference posso assegnare il valore null, ad un tipo primitivo non posso assgenare un valore null altrimenti incorrerò ad un errore di compilazione



**- Declaring and initializing Variables**

{access modifier} {type} {name} = {initialization};

```java
String variable;

public int variable = 1;
```



\- **Declaring Multiple Variables**

E' possibile dichiarare più variabili in un unico statment, tutte le variabili devono condividere la stessa definizione del tipo, ogni dichiarazione è suddivisa da una virgola, dopo ogni virgola posso definire il nome della sua variabile e se necessario inizializzare la variabile.

```java

String v1, v2; //compile

String v1 = "test", v2; //compile

int x, y, z = 0; //compile

int x, double y; // does not compile - all'interno del singolo statment la definizione del tipo deve essere unica

int x; double y; // compile - si tratta di due statment differenti

int x; i = 0; // does not compile

```



\- **Indentiier**

In java esistono delle regole da rispettare per i nomi degli identifier, queste di applicano a tutto ciò a cui viene dato un nome: package, class, method, variable. Le regole sono le seguenti:

- gli identifier devono iniziare con lettere o con i simboli $, _
- a parte il primo carattere gli identifier possono contenere lettere, numeri, i simboli $, _
- gli identifier non possono essere keywords, essendo java case-sensitive se una keywords presenta caratteri maiuscoli è possibile usarla come identifier, i valori literal 'null', 'false', 'true' non sono delle keywords ma non è comunque possibile usarle come identifier, il compilatore restituirà un errore



**- Default Initialization of Variables**



**- Local Variables**



- Le variabili locali sono quelle definite all'interno di un metodo, anche i parametri di input di un metodo sono local variables
- devono essere inizializzate prima di essere usate in un espressione, altrimenti il compilatore restituisce un errore
- possono essere dichiarate senza inizializzazione ed essere inizializzate in uno statment successivo:
  *int x;x = 1;int y = x;*
- Il compilatore tiene conto dell'inizializzazione delle variabili locali anche se questa avviene all'interno di rami di un *if* o di un *for*, se la variabile non viene inizializzata in tutti i rami raggiungibili il compilatore solleverà un errore in fase di compilazione. (da verificare la casistica di rami non raggiungibili) Attenzione!, il compilatore tiene conto dei branch creati tramite degli if, ma è in grado di valutare le condizioni solamente gli operandi sono noti, ovvero literal o costanti.
- le variabili locali possono essere *final*



**- Instance e Class Variables**



- Le variabili di istanza sono tutte le variabili che si trovano al di fuori dei metodi ma all'interno di una classe e non presentano la keyword *static*  all'interno della loro definizione
- Le variabili di classe seguono le stesse regole delle variabili di istanza ma presentano la keyword *static* nella loro definizione
- Sia le variabili di instanza che di classe non necessitano dell'inizializzazione per essere utilizzate in quanto il compilatore le inizializza con dei valori di default:



| boolean                | false          |
| ---------------------- | -------------- |
| byte, short, int, long | 0              |
| float, double          | 0.0            |
| char                   | '\u0000' (NUL) |
| Reference Type         | null           |





**- Variable Scope**



Ogni variabile ha il proprio scope, ovvero ambito di validità, a seconda della tipologia di variabile lo scope di una variabile può essere più o meno ampio.



- **Class Variable:** lo scope parte dalla definizione della variabile e si chiude al termine del programma
- **Instance Variable:** lo scope parte dalla definizione della variabile e si chiude nel momento in cui l'istanza dell'oggetto nel quale è definita la variabile non viene passata al garbage collector
- **Local Variable:** lo scope parte dalla definizione della variabile e si conclude alla chiusura del code block nel quale è stata definita la variabile



Se si prova a far riferimento ad una variabile al di fuori del proprio scope il compilatore solleverà un errore. Da uno scope più interno si può far riferimento ad una variabile definita in uno scope più esterno ma non viceversa.



**- Ordering elements in a Class**



| package | not required | first line                               |
| ------- | ------------ | ---------------------------------------- |
| import  | not required | immediately after the package definition |
| class   | required     | immeditely afetr the imports definition  |
| fields  | not required | anywhere inside the class                |
| methods | not required | anywhere inside the class                |



- I commenti posso essere inseriti ovunque e non devono rispettare alcun ordine ne influiscono con l'ordine degli altri elementi.
- Anche nel caso vi siano più definizioni di classi all'interno dello stesso file la definizione del package e degli imports devono essere posti come primi  elementi all'interno del file



**- Destroying Objects**



**- Garbage Collection**



riguardo il garbage collector è necessario sapere due cose per l'esame:



- System.gc() - un metodo messo a disposizione dalle api standard di java, che fa pensare sia possibile far eseguire la garbage collection, ma in realtà questo metodo semplicemente suggerisce l'esecuzione del garbage collector, ma la jvm può ignorare il suggerimento.
- Il momento in cui un oggetto diviene eligibile alla garbage collection e quindi alla sua cancellazione dal heap coincide con:
  - quando non esiste più nessun reference type che punta all'oggetto
  - quando tutte le refecence type che puntano all'oggetto vanno out of the scope



Deve essere molto chiara la differenza tra la reference type e l'object instance:



- Una reference type è una variabile che contiene il puntatore ad un istanza di oggetto, può risiedere o non risiedere all'interno del heap, ha un nome ed ha una dimensione fissa
- Un'istanza di oggetto risiede sempre nel heap, non ha un nome e non può essere acceduta se non attraverso la sua reference, la sua dimensione dipende dalla sua definizione di classe



**- Finalize**



Java consente l'implementazione di un metodo *finalize()*, questo metodo viene richiamato quando la jvm prova ad eseguire la garbage collection per l'oggetto.



- il metodo *finalize* può non essere invocato affatto
- non viene mai invocato due volte, se la jvm prova ad invocarlo una prima volta senza riuscire ad eseguire il collect per l'oggetto non tenterà di invocare il metodo *finalize()* una seconda volta



**- Benefits of Java**



- **Object Oriented**
- **Encapsulation**
- **Platform Independant** (write once, run everywhere)
- **Robust** (no memory leaks)
- **Simple** (no pointer)
- **Secure** (jvm sandbox)