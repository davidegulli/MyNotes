# Methods and Encapsulation



**- Designing Methods**



Method Declaration:



*public                     final                           void                 nap                      (int param)            throws Exception             { }*

**access modifier    optional specifier     return type     method name     parameter list    exception (optional)     method body**





| Element            | Example Value    | Required               |
| ------------------ | ---------------- | ---------------------- |
| Access Modifier    | public           | No                     |
| Optional Specifier | final            | No                     |
| Return Type        | void             | Yes                    |
| Method Name        | nap              | Yes                    |
| Parameter List     | (int param)      | Yes (può essere vuota) |
| Exception          | throws Exception | No                     |
| Method body        | {}               | Yes (può essere vuoto) |



**- Access Modifier**



- *private -* il membro può essere acceduto solamente internamente dalla classe che lo dichiara
- *default -* il membro può essere acceduto internamente dalla classe che lo dichiara e dalle classi che si trovano all'interno dello stesso package
- *protected -* il metodo segue le stesse regole di accesso di *default* ma inoltre può essere acceduto dalle subclasses
- *public -* il metodo può essere acceduto da qualsiasi classe che compone il programma



**- Optional Specifier**



La dichiarazione di un metodo può avere zero o più optional specifier, anche se alcune combinazioni non sono consentite, se ci sono più optional specifier questi possono essere messi in qualsiasi ordine.



- *static -* dichiarazione di un method class
- *abstract -* dichiarazione di un metodo che non possiede un body
- *final -* dichiarazione di un metodo che non può essere soggetto ad overriding
- *syncronized -* argomento di ocp
- *native -* argomento non trattato
- *strictfp -* argomento non trattato



**- Return Type**



- un metodo può restituire un qualsiasi java type, primitivi o oggetti
- deve obbligatoriamente specificare nella sua dichiarazione un return type, se non restituisce alcun valore si usa la keyword *void*
-  se restituisce un java type, nel corpo del metodo deve essere presente un *return* che restituisca un java type compatibile con quello dichiarato nella dichiarazione del metodo. Il compilatore è abbastanza intelligente per individuare se lo statment di return è in un branch del codice non raggiungibile.
- se il metodo dichiara un return type *void,* nel corpo del metodo può essere presente lo statment *return;* vuoto o non esserci affatto



**- Method Name**



- Il nome del metodo segue le stesse regole degli altri identifier



**- Parameter List**



- è sempre richiesto che siano presenti le parentesi tonde, ma al loro interno possono anche non contenere nulla
- possono essere presenti zero o n parametri specificati dal loro java type e dal nome del parametro separati dalla virgola



**- Optional Exception**



- possono essere presenti zero o più eccezioni che possono essere sollevate dal metodo



**- Method Body**



- sostanzialmente è un blocco di codice che può contenere zero o più statment



**- Working with Varargs**



- nella parameter list può essere presente un parametro nella forma di varargs.
  - per ogni metodo può essere presente un solo varargs
  - il varargs deve essere l'ultimo parametro
- nella fase di invocazione al parametro varargs può essere passato:
  - un array dello stesso tipo del parametro
  - l'elenco dei parametri
  - il parametro può essere omesso, il compilatore creerà un array vuoto che sarà passato al metodo
  - null, in questo caso se nel metodo non vengono inseriti degli opportuni controlli sui valori null si corre il rischio di incappare in eccezioni di tipo NullPointerException



**- Applying Access Modifiers**



**- Private Access**



I membri *private* di una classe possono essere acceduti solamente da codice presente all'interno della loro stessa classe



\- **Default Access**



Se i membri di una classe non presentano un access modifier viene loro assegnato il default access, detto anche private package access.



I membri di una classe che hanno il default access possono essere acceduti dal codice presente in tutte le classi dello stesso package.



**- Protected Access**



I membri *protected* di una classe possono essere acceduti dal codice presente nelle classi appartenenti allo stesso package e dal codice presente nelle subclasses.



E' necessario fare un'importante distinzione nelle modalità di accesso ai membri protected, questi possono essere acceduti:

- in maniera diretta all'interno di subclasses, richiamando direttamente il metodo sfruttando l'eriditarietà
- in maniera indiretta usando una variabile e quindi una reference ad un oggetto



In questo secondo caso è necessario fare attenzione a non cadere in sottili tranelli:



Bird.java



package pond.shore;



public class Bird {

​     protected String text = "floating";

​     protected void floatingInWater() {

​         System.ou.println(text);

​     }

}





Swan.java



package pond.swan;



import pond.shore.Bird;



public class extends Bird {



​     public void swim(){

​         floatingInWater(); // metodo ereditato accessibile perchè protected

​          System.out.println(text); // attributo ereditato accessibile perchè protected

​     }



​     public void helpOtherSwanSwim(){

​         Swan swan = new Swan(); //

​         swan.floatingInWater(); // uso una reference a Swan che è la stessa classe, tramite

​                                 // ereditarietà accedo al metodo di Bird perchè questo è protected

​         System.out.println(swan.text); // uso una reference a Swan che è la stessa classe, tramite

​                                        // ereditarietà accedo al metodo di Bird perchè questo

​                                        // è protected

​     }



​     public void helpOtherBirdSwim(){

​         Bird bird = new Bird();

​         bird.floatingInWater(); // does not compile - swan non è nello stesso package di bird,

​                                 // è possibile accedere ai metodi protected solamente tramite

​                                 // ereditarietà

​         System.out.println(bird.text); // does not compile come sopra

​     }



​     public void helpOtherBirdSwim2(){

​         Bird bird = new Swan();

​         bird.floatingInWater(); // does not compile - la reference è di tipo Bird, quindi

​                                 // quindi l'interfaccia è Bird e non è possibile accedere ai suoi

​                                 // membri protected se non tramite ereditarietà o se le classi non

​                                 // si trovano nello stesso package

​         System.out.println(bird.text); // does not compile comee sopra

​     }

}



**- Public Access**



Un membro *public* può essere acceduto da qualsiasi classe senza alcuna restirzione.





| Can Access                         | private member | deafult member | protected member | public member |
| ---------------------------------- | -------------- | -------------- | ---------------- | ------------- |
| same class                         | Yes            | Yes            | Yes              | Yes           |
| different class, same package      | No             | Yes            | Yes              | Yes           |
| different package, super-class     | No             | No             | Yes              | Yes           |
| different package, non super-class | No             | No             | No               | Yes           |





**- Design Static Methods And Fields**



I membri di una classe definiti come statici sono membri di classe e non di istanza, quindi esistono anche se non è stata creata nessuna istanza dell'oggetto che li contiene. Questi si possono dire condivisi con tutte le istanze di una classe.



Sono utili per diverse ragioni tra cui:

- Metodi di utilità che non lavorano sullo stato dell'oggetto e quindi sulle sue instance variable, un metodo statico può essere invocato senza la necessità di istanziare un oggetto.
- Mantenere uno stato unico e condiviso con tutte le istanze di un oggetto, ad esempio un counter.



Nota:

Una piccola nota sulle strategie di memorizzazione java dei dati e del codice, java memorizza una copia dei dati contenuti in variabili per singola istanza di oggetto, mentre il codice presente all'interno di un metodo ha un sola copia condivisa per tutti le istanze di oggetto, nelle fasi di esecuzione di un metodo le variabili locali vengono memorizzate all'interno di una area detta stack per il tempo necessario.



**- Calling a Static Variable or Method**



Le chiamate a metodi o variabili statiche sono molto semplici è sufficiente anteporre il nome della classe che contiene il membro statico.



E' comunque possibile richiamate un membro statico usando la reference ad un istanza di oggetto, addirittura è possibile farlo anche se il valore della reference è null.



Koala k = new Koala();

System.out.printl(k.count); // java verifica che count è statico e lo invoca come Koala.count

k = null;

System.out.printl(k.count); // come detto sopra viene invocato come Koala.count quindi non viene

​                            // sollevata alcuna eccezione



**- Static vs. Instance**





| Type            | Calling                 | Legal |
| --------------- | ----------------------- | ----- |
| Static member   | Another Static member   | Yes   |
| Static member   | Another instance member | No    |
| Instance member | Another static member   | Yes   |
| Instance member | Another instance member | Yes   |



**- Static Variables**



private static int counter = 0; // possono essere inizializzate come le variabili non statiche



private static final NUM_COUNTERS = 0; // dichiarazione di una costante

NUM_COUNTERS = 1; // does not compile - le costanti final possono essere inizializzate una sola volta



Le costanti danno la possibilità di avere delle variabili che non ammettono riassegnazioni del proprio valore, ma questo ovviamente non vuol dire che in caso di una object referece il suo stato non possa cambiare.



private static final ArrayList<String> LIST = new ArrayList<>();

LIST.add("test"); // it compiles



**- Static Initialization**



Static Initializer viene richiamato una ed una sola volta nel momento in cui la classe viene richiamata per la prima volta.



private static int one;

private static int two;

private static int three = 3;

private static int four; // does not compile la variabile non viene mai inizializzata



static {

​     one = 1;

​     two = 2;

​     three = 3; // does not compile la variabile è già stata inizializzata

​     two = 4; // does not compile la variabile è già stata inizializzata

}



- In uno *static* *initializer* non è possibile fare il throw di un eccezzione, altrimenti il compilatore solleverà un errore: initializer must be able to complete normally



**- Static Imports**



Gli static import consentono di usare dei membri statici di una classe senza il bisogno di specificare il nome della classe, questo perchè viene specificato nello static import:



import static java.util.Arrays.asList



- l'oridne delle keyword è obbligatoriamente *import static,* non può essere diverso
- se vengono importati due membri statici che hanno lo stesso nome ma appartenenti a due classi differenti il compilatore segnalerà un errore
- se nella classe dove viene definito l'import statico esiste un membro con lo stesso nome del membro importato staticamente, in fase di invocazione verrà data priorità al membro definito all'interno della classe
- è possibile usare la wildcard * per importare tutti i membri statici di una classe
- la dichiarazione *import static si può usare* solamente per l'importazione di membri statici e nient'altro



Un caso molto particolare: in caso di ambiguità sui nomi degli import statici di metodi con lo stesso nome di metodi presenti all'interno della classe, il compilatore ignora completamente l'import statico anche quando i parametri dei metodi sono differenti.



import java.util.List;

import java.util.Arrays;

import static java.util.Arrays.asList;



class Main {



​    static List asList(String[] array){

​        System.out.println("Main.asList()");

​        return null;

​    }



​    public static void main(String[] args){

​        Object[] array = {"1", "2", "3"};

​        List list = asList(array); // does not compile: error: incompatible types: Object[] cannot be

​                                   // converted to String[]

​    }



}



**- Passing Data Among Methods**



Java nell'invocazione dei metodi per i parametri del metodo usa un approccio pass-by-value, ciò vuol dire che al metodo viene passata una copia del valore del parametro di input.



Ciò comporta che:

- se all'interno del metodo eseguo una riassegnazione del valore della local vabiable del parametro, il chiamante continuerà ad avere il valore originale della variabile passata come parametro, ciò vale per  i primitivi come per le object reference
- se all'interno del metodo invoco un metodo di una object reference ricevuta come parametro, viene modificato lo stato dell'oggetto puntato dalla reference, il cambiamento di stato sarà visibile anche dal chiamante
- I return seguono le loro normali regole



**- Overloading Methods**



L'overloading di un metodo si basa sulla differenza della parameter list, i parametri possono differire:

- per tipologia
- per numero
- per ordine



La differenza di accesse modifier, optional specifier, return type o exception non comportano overloading, ma in caso ci sia overloanding grazie alla differenza della parameter list è possibile variare anch'essi.



**- Overloading and Varargs**



public void fly(int[] lengths) { }

public void fly(int... lengths) { } // does not compile



I varargs sono trattati a tutti gli effetti come array quindi come si può vedere dall'esempio precedente le due dichiarazioni dei metodi vengono viste dal compilatore come uguali anche se apparentemente non lo sono.



**- Autoboxing**



public void fly(int num) { }

public void fly(Integer num) { }



public static void main(String args...){

​     fly(3);

}



Nella casistica precedente java invocherà il metodo *fly(int num)*, come regola java cerca di invocare i metodi con una corrispondenza più esatta possibile, quindi in presenza di un metodo che vuole un int come parametro chiamerà quello, se fosse assente eseguirebbe l'autoboxing ed invocherebbe la versione *fly(Integer num)*.



**- Refercence Type**



Data la regola precedente per cui java cerca di invocare sempre il metodo con una corrispondenza più esatta:



public class ReferenceTypes {



​     public void fly(String str) {

​          System.out.println("String");

​     }



​     public void fly(Object obj){

​          System.out.println("Object");

​     }



​     public static void main(String args[]){

​          ReferenceTypes rt = new ReferencesType();

​          rt.fly("test"); // it prints String

​          rt.fly(56); // it prints Objects Java cerca una corrispondenza per int, non trovandola

​                      // esegue l'autoboxing ad Integer, non trovando ancora una corrisposndenza

​                      // va su Object

​     }



}



**- Primitives Type**



Nuovamente valgono le stesse regole, java cercherà di invocare il metodo con la corrispondenza maggiore, se non la trova cerca un metodo che accetti un parametro compatibile e di dimensioni maggiori.



Ad esempio:



public class Plane {



​    public void fly(long num){

​         System.out.println("long");

​    }



​    public static void main(String[] args){

​         Plane plane = new Plane();

​         plane.fly(123);  // prints long il metodo accetta un int perchè di dimensioni inferiori a long

​         plane.fly(123L); // prints long corrispondenza esatta

​         plane.fly(125.54); // does not compile non è possibile passare un tipo di dimensioni maggiori

​    }

}



**- Putting It All Together**





| Rule                   | Example of what will choosen for *glide(1,2);* |
| ---------------------- | ---------------------------------------------- |
| Exact Match            | *glide(int i, int y);*                         |
| Larger primitive match | *glide(long x, long y);*                       |
| Autoboxing match       | *glide(Integer x, Integer y);*                 |
| Varargs match          | *glide(int... params);*                        |



Questa tabella rappresenta l'ordine con cui java effettua le verifiche per cercare la più esatta corrispondenza.



Attenzione, java è in grado di effettuare una sola conversione, non può effettuare un salto ad esempio da un primitivo differente ad un autoboxing.



public class Plane {



​    public void fly(Long num){

​         System.out.println("long");

​    }



​    public static void main(String[] args){

​         Plane plane = new Plane();

​         plane.fly(123); // does not compile, java convert il paramento in long non è in grado di fare

​                         // autoboxing per ricercare la corrispondenza con *fly(Long num);*

​         plane.fly(123L); // prints long corrispondenza esatta



​    }

}



In caso di over-loading  di metodi che prendono come input oggetti quando viene passato come parametro null viene invocato il metodo con il parametro più specifico:



public class TestClass{

   public void method(Object o){

​      System.out.println("Object Version");

   }

   public void method(java.io.FileNotFoundException s){

​      System.out.println("java.io.FileNotFoundException Version");

   }

   public void method(java.io.IOException s){

​      System.out.println("IOException Version");

   }

   public static void main(String args[]){

​      TestClass tc = new TestClass();

​      tc.method(null); // Viene invocato il metodo: public void method(java.io.FileNotFoundException s)

   }

}



**- Creating Constructors**



public class Bunny {



​     public Bunny(){

​          System.out.println("BUNNY");

​     }

}



- La keyword *this* viene utilizzata per accedere alle varibili d'istanza della classe, di solito necessaria quando i parametri di input di un costruttore hanno gli stessi nomi delle variabili d'istanza della classe



**- Defaul Constructor**



Un *default constructor* è un costruttore che non ha parametri ed ha un body vuoto, questo viene generato automaticamente in fase di compilazione quando per la classe non è stato dichiarato alcun costruttore.



Un costruttore con access modifier *private* non può essere richiamato da altre classi, questo comporta che la classe non è istanziabile al di fuori di se stessa.



**- Overloading Constructor**



In una classe possono esserci più costruttori in overloading, così come per i metodi, per essi può variare solamente la lista di parametri, seguendo le stesse regole già viste per l'overloading dei metodi.



- spesso per evitare duplicazione di codice si effettuano chiamate a catena di costruttori
- un costruttore all'interno di una classe può essere invocato come segue:



​     class Costructor {



​          public Costructor(int x){

​               this(x, 15); // deve sempre essere il primo statment non commentato all'interno del

​                            // costruttore

​          }



​          public Costructor(int x, int y){

​               this(x, y);

​          }

​     }

- se si tenta di richiamare un construttore all'interno di un altro costruttore usando la keyword new non si avrà il risultato sperato, ovvero verrà creato una nuova istanza di oggetto che però verrà ignorata e quindi non avrà alcun effetto sullo stato dell'oggetto corrente



​     class Costructor {



​          public Costructor(int x){

​               new Constructor(x, 15); // crea una nuova istanza dell'oggetto ma questa viene ignorata

​          }



​          public Costructor(int x, int y){

​               this(x, y);

​          }

​     }



- l'istruzione this() può essere codificato solamente come prima riga di un costruttore e da nessun altra parte



**- Final Fields**



Come si è già visto le variabili final sono delle costanti che devo essere inizializzate esattamente una sola volta. L'inizializzazione può essere fatta anche all'interno di un costruttore.



La costanti final static possono essere inizializzate solamente nella dichiarazione della costante o in static inatializers



Il compilatore è molto intelligente, è in grado di verificare se due diversi statment di inizializzazione di una variabile final possono essere raggiunti entrambi in fase di compilazione o meno, sollevando un errore nel primo caso:



public class Plane {



​    public final String TEST;



​    public Plane(){

​        TEST = "test"; // compile per ogni istanza può essere eseguito una sola volta

​    }



​    public Plane(int num){

​        TEST = "test1"; // compile per ogni istanza può essere eseguito una sola volta

​    }



​    public static void main(String[] args){

​         Plane plane = new Plane();

​    }

}



mentre invece:



public class Plane {



​    public final String TEST;



​    public Plane(){

​        this(1);

​        TEST = "test"; // does not compile, l'assegnazione viene effettuata nella chiamata precedente

​    }



​    public Plane(int num){

​        TEST = "test1";

​    }



​    public static void main(String[] args){

​         Plane plane = new Plane();i

​    }

}



**- Order of Inizialization**



1. inizializzazione della super class
2. esecuzione static variable e static initializer blocks, nel loro ordine di dichiarazione
3. esecuzione instance variable e instance initializer blocks, nel loro ordine di dichiarazione
4. esecuzione constructors



Esempio:



class A{

   A() {  print();   }

   void print() { System.out.println("A"); }

}



class B extends A{

   int i =   4;

   public static void main(String[] args){

​      A a = new B();

​      a.print();

   }

   void print() { System.out.println(i); }

}



/* when the progma run the result is: 0 4 */

/* Quando viene invocato il costruttore '*new B()*' la classe A viene inizializzata e quindi viene invocato il suo costruttore questo dove è presente l'invocazione del metodo *print()* che in ovveriding e quindi viene usata l'implementazione fornita dalla classe B, questa ancora non è stata inizializzata, quindi la variabile *i* ancora non è stata inizializzata, quindi il metodo stampa 0, poi seguendo il normale flusso viene stampato 4 in quanto la seconda invocazione del metodo *print()* avviene dopo l'inizializzazione della classe B.





**- Writing Simple Lambdas**



In java 8 sono stati aggiunti degli elementi di *functionl programming*, un approccio diverso da quello orientato agli oggetti.



Le *lamba expression* sono dei blocchi di codice che possono essere passati come parametri a dei metodi, possono essere visti come dei metodi anonimi, ovvero che non hanno nome.



Le *lambda expression*  usano il concetto di *deffered execution*, il codice viene specificato in un dato momento ma viene utilizzato in un momento successivo.



**- Lambda Syntax**



La sintassi di un espressione lambda può variare di molto, ci sono diverse parti opzionali che possono essere omesse nell espressioni più semplici.



Innanzi tutto è importare ricordare che le lamba expression più semplici sono mappate per il seguente modello di interfacce:



boolean test(Object a);



La sintassi più semplice è la seguente:



a -> a.canHop()



la versione più verbosa è la seguente:



(Animal a) -> {return a.canHop();}



La struttura di base è sempre la stessa:



1. La lista dei parametri
   1. Il tipo dei parametri è opzionale, il compilatore è in grado di recuperare la tipologia dei parametri dall'interfaccia che sta mappando
   2. Possono essere passati zero o n parametri
   3. Le parentesi tonde diventano opzionali se è presente un solo parametro e se non è specificata la tipologia del parametro
2. L'operatore -> che divide i parametri dal corpo dell'espressione
3. Il corpo dell'espressione
   1. Se sono presenti le parentesi graffe la presenza della keyword *return* e del carattere ; è obbligatoria
   2. Le parentesi graffe sono opzionali e possono essere omesse se il corpo dell'espressione presenta un solo statment
   3. Nel corpo dell'espressione non è possibile ridefinire una variabile esistente:



​           (a,b) -> {int a = 0; return 5;} // does not compile



Esempi validi:



print(() -> true);

print(a -> a.startWith("test"));

print((String a) -> a.startWith("test"));

print((a,b) -> a.startWith("test"));

print((String a, String b) -> a.startWith("test"));



Esempi non validi:



print(a,b -> a.startWith("test")); // does not compile

print(a -> { a.startWith("test"); }); does not compile

print(a -> { return a.startWith("test") }); //does not compile



**- Predicates**



Le Lambdas expression lavorano sempre su interfacce che hanno un solo metodo astratto, ma possono contenere uno o n metodi static o default queste vengono chiamate *functional interface.* Per evitare che ogni qual volta si usi una lambdas ci sia bisogno di creare un'interfaccia, java mette a disposizione delle interfacce già pronte che modellano delle problematiche comuni.



Per l'esame OCA è necessario conoscere l'interfaccia:



java.util.functional.Predicate



public interface Predicate<T> {

​     boolean test(T t);

}



Java usa quest'interfaccia all'interno delle proprie API per consentire l'uso delle lambdas con le proprie classi, ad esempio:



ArrayList.removeIf(Predicate<? super E> filter);



Che consente di eliminare degli elementi da un'array list secondo il test implementato dalla lambdas