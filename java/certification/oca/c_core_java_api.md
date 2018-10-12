# Core Java Api



**Creating and Manipulatimg Strings**



L'oggetto stringa in java è una sequenza di caratteri immutabile.

Una variabile di tipo String può essere inizializzata in un due diversi modi:



String name = "Davide"; // Literal viene memorizzato nell StringPool della jvm

String name = new String("Davide"); // New object instantiation viene memorizzato nell'heap come ogni altro oggetto



**- Concatenation**



Regole:



- Se entrambi gli operandi della concatenazione sono numerici il risultato sarà l'addizione tra i due operandi
- Se uno degli operandi è di tipo String il risultato sarà una concatenazione di stringhe
- L'espressione si calcola sempre da sinista verso destra
- Se uno dei due operandi della concatenazione è un oggetto String e l'altro un object di qualsiasi tipo su quest'ultimo verrà invocato il metodo toString(), il risultato sarà poi usato per la concatenazione



int three = 3;

String four = "4";

System.out.print( 1 + 2 + three + four ); // it prints the string "64" 



/* Object concatenation */

LocalDate d3 = LocalDate.now();

String out = new StringBuilder("test") + d3 + "test"; // does not compile

String out = new StringBuilder("test") + "test" + d3; // compile

System.out.println(out);



E' possibile usare anche l'operatore += per la concatenazione tra stringhe, questo segue le regole valide per le tipologie numeriche:



String s = 1;

s += "2" // it is equivalent to s = s + "2";



**- Immutability**



String è immutabile ciò vuol dire che una volta creato un oggetto di tipo String questo non potrà essere modificato in alcun modo.

La classe String ha solamente metodi che restituiscono un nuovo oggetto di tipo String, ma nessun metodo che consenta la modifica della stringa contenuta dall'istanza di oggetto.



Fare attenzione alla seguente tipologia di trick:



String s1 = "1";

String s2 = s1.concat("2");

s2.concat("3");

System.out.print(s2); // it prints "12"



**- String Pool**



Tutte gli oggetti di tipo String creati via literal occupano uno spazio di memoria riservato chiamato internal pool o string pool, all'interno del quale non possono esistere duplicazioni.



Gli oggetto di tipo String creati via costruttore ( new String("xyz") ) occupano spazio di memoria dell'heap



Da tutto ciò ne consegue che:



String s1 = "test";

String s2 = "test";

String s3 = new String("test");



System.out.println(s1 == s2); // it prints true

System.out.println(s1 == s3); // it prints false



//Esempio particolare:

String str1 = "one";

String str2 = "two";

System.out.println( str1.equals(str1=str2) ); // prints false il primo str1 viene valutato prima della sua assegnazione



**- Important String Method**



E' bene ricordare che una stringa altro non è che una sequenza di caratteri, il primo carattere ha indice 0.



| A    | N    | I    | M    | A    | L    | S    |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| 0    | 1    | 2    | 3    | 4    | 5    | 6    |



Method:



- **length()**

- **\*charAt()***se si passa come parametro un intero che non rientra nel range degli indici contenuti nella stringa verrà sollevata la seguente eccezzione:
  java.lang.StringIndexOutOfBuondsException: String index out of the range
  (sia negativo che positivo, ad esempio con -1 otterrà sempre eccezione)

- **\*indexOf()***

​     int indexOf(char ch)

​     int indexOf(char ch, int fromIndex) // la ricerca parte dal indice indicato incluso

​     int indexOf(String ch)

​     int indexOf(String ch, int fromIndex)

​          

​     String s = "animals";

​     System.out.println(s.indexOf('a')); // 0

​     System.out.println(s.indexOf('al')); // 4

​     System.out.println(s.indexOf('a', 4)); // 4

​     System.out.println(s.indexOf('al', 5)); // -1 



- **\*substring()***

​     String substring(int beginIndex) // seleziona dall'indice fornito compreso fino al termine

​                                      // della stringa  

​     String substring(int beginIndex, int endIndex) // selezione dall'indice iniziale compreso

​                                                    // fino all'indice finale escluso     



​     String s = "animals";

​     System.out.println(s.substring(3)); // "m"

​     System.out.println(s.substring(3,4)); // "m"

​     System.out.println(s.substring(3,7)); // "mals"



​     System.out.println(s.substring(3,3)); // ""

​     System.out.println(s.substring(3,2)); // throws an exception l'indice iniziale non può

​                                           // essere maggiore di quello finale

​     System.out.println(s.substring(3,8)); // throws an exception l'indice finale non può

​                                           // essere maggiore di s.length()



- **\*toLowerCase() / toUpperCase()***

- **\*equals() / equalsIgnoreCase()***

- **\*startsWith() / endsWith()***Restituisce un boolean, è case sensitive

- **\*contains()***Restituisce un boolean, è case sensitive

- **\*replace()***

​     String replace(char olderChar, char newChar)

​     String replace(CharSequence oldChars, CharSequence newChars)



​     System.out.printl("abcabc".replace('a','A')); // prints AbcAbc

​     System.out.printl("abcabc".replace("a","A")); // prints AbcAbc



​         CharSequnce è un interfaccia implementata sia da String che da StringBuilder



​          Se i char di input passati come parametri sono identici, viene restituito lo stesso oggetto String al quale è stato applicato il metodo:



​        "String".replace('g','g') == "String" // it return true  



- **\*trim()***



**- Method Chaining**





String result = "AnImAlS   ".trim().toLowerCase().replace("a","A");

System.out.println(result); // prints Animals



Metodi invocati a catena come in questo caso devono essere letti ed eseguiti sempre da sinistra a destra.

Essendo String immutabile l'oggetto su cui vengono invocati metodi a catena non cambia il proprio stato.



\- **Using the StringBuilder Class**



- La classe StringBuilder a differenza di String è mutabile, ciò vuol dire che i suoi metodi consentono di cambiare lo stato dell'oggetto.
- L'utilità della classe StringBuilder è la possibilità di risparimare lavoro alla JVM nelle operazioni di concatenazione di stringhe, consentire di fare append di stringhe su un unico oggetto anzichè, come per glil oggetti di tipo String, dover creare ad ogni nuova concatenazione un nuovo oggetto di tipo String.
- Il metodo .append() restituisce la reference dell'oggetto StringBuilder su cui è stato invocato il metodo, quindi la reference dell'oggetto già mutato dall'invocazione del metodo, è necessario fare attenzione a questa differenza tra String e StringBuilder, String restituisce sempre un nuovo oggetto, StringBuilder restituisce il riferimento a se stesso, questo è importante nelle invocazioni a catena dei metodi delle due tipologie di oggetti.
- Sia la classe StringBuilder che la classe StringBuffer sono *final*



​     StringBuilder a = new StringBuilder("abc");

​     StringBuilder b = a.append("de");

​     b = b.append("f").append("g");

​     System.out.println("a=" + a); // it prints "abcdefg"

​     System.out.println("b=" + b); // it prints "abcdefg"

​     System.out.println(a == b); // true



**- Creating a StringBuilder**



StringBuilder sb1 = new StringBuilder(); // non contiene nessuna stringa quindi size a 0 e capacity di default 16

StringBuilder sb2 = new StringBuilder("animals"); // contiene la stringa passata al costruttore, size = 7, capacity = 16

StringBuilder sb3 = new StringBuilder(10); // non contiene nessuna stringa quindi size = 0, capacity = 10



**- StringBuilder Metods**



- **\*length() / indexOf() / charAt() / substring()***Questi metodi assumo gli stessi comportamenti dei rispettivi metodi della classe String
  Attenzione solamente al metodo *substring()* restituisce una stringa, quindi non cambia lo stato dell'oggetto, si tratta di un metodo di inquiry.

- **\*append()***Concatena la stringa passata come parametro a quella contenuta nell'oggetto StringBuilder e poi restituisce la reference all'oggetto StringBuilder corrente

- **\*insert()***Inserisce una stringa all'indice passato come parametro

​     StringBuilder insert(int offset, String str)



​     StringBuilder sb = new StringBuilder("animals");

​     sb.insert(7, "-"); // animals-

​     sb.insert(0, "-"); // -animals-

​     sb.insert(4, "-"); // -ani-mals-



- **\*delete() / deleteCharAt()***Elimina caratteri all'interno dello StringBuilder:

​     StringBuilder delete(int startIndex, int endIndex)



​     StringBuilder sb = new StringBuilder("abcdef");

​     sb.delete(1,3); // adef

​     sb.deleteCharAt(5); // throws an exception la dimensione della string e minore di 6



- **\*reverse()***Inverte i caratteri contenuti nell'oggetto StringBuilder

​     StringBuilder reverse()



- **\*toString()***Restituisce una stringa composta dalla sequenza di caratteri contenuta nell'oggetto StringBuilder.

​     String toString()



**- StringBuilder vs StringBuffer**



La classe StringBuffer fa esattamente le stesse cose della classe StringBuilder ma è più lento in quanto è thread-safe, quindi sincronizzato.



**- Understanding Equality**



- == testa l'uguaglianza dei riferimenti di due variabili, se due variabili puntano allo stesso oggetto viene restituito true
- .equals() è un metodo della classe Object se non viene reimplementato da un oggetto specifico anch'esso testa i riferimenti di due variabili 
- La classe String reimplementa il metodo .equals() per verificare che i due oggetti String contengano la stessa sequenza di caratteri
- La classe StringBuilder non reimplementa il metodo .equals() quindi questo testa se due variabili puntano allo stesso oggetto di tipo StringBuilder



Attenzione ad alcuni casi della classe String, sappiamo che tutti i literal vengono conservati in un pool, ma questo avviene solamente per i literal presenti in fase di compilazione, e non per quelli calcolati a runtime, ad esempio:



String x = "Hello World";

String y = " Hello World".trim();

System.out.print(x == y); // it prints false



**- Understanding Java Arrays**



**- Creating Arrays**



Esistono diverse sintassi per definire ed istanziare oggetti di tipo arrays:



int[] array = new int[3];



in questo caso viene definita una variabile di tipo *int[]*  che conterrà il riferimento ad un array di interi che avrà dimensione 3, ciò vuol dire che potrà contenere 3 elementi di tipo int. Con questa tipologia di inizializzazione viene creato un array con tutti gli elementi inizializzati al loro valore di default, quindi in questo caso, essendo elementi di tipo int il loro valore sarà 0.



int[] array = new int[] {4,5,6};



viene creato un array con gli elementi valorizzati con i valori passati in input all'interno delle {}



int[] array = {4,5,6};



equivale a quanto detto in precedenza, questa tipologia di inizializzazione viene indicata come anonymous array.

L'inizializzazione attraverso l'anonymous array può essere usato solo nell'istruzione di dichiarazione di un array.





Sono valide anche le seguenti dichiarazioni:



int [] array;

int    [] array;

int array[];

int array [];

int array        [];

int array

[];  // perfino questa.



Come per le variabili normali è possibile dichiarare più variabili di tipo [] nello stesso statment:



int[] arr1, arr2;

int[] arr1 = {1,3}, arr2 = {2,4,6};



int arr1, arr2[]; // ATTENZIONE creerà una variabile di tipo int e una di tipo int[].



**- Creating Array with Reference Variables**



- E' possibile creare array con qualsiasi tipo java compresi quelli custom sviluppati da noi.
- La differenza tra un array di primitivi ed uno reference è che gli elementi di un array di primitive conterranno un valore, mentre un array di reference conterrà a la reference ad un oggetto e non l'oggetto.
- E' possibile fare il casting anche per gli array ma è necessario far attenzione, una variabile array di tipo super class può contenere un array di una sua sub class, ma mai il contrario, inoltre possono verificarsi eccezioni anche se non si usa il tipo corretto per l'assegnazione di oggetti agli elementi dell'array:



​     String[] strings = {"strings"};

​     Objects[] objects = strings;

​     String[] againStrings = (String[]) objects;

​     againStrings[0] = new StringBuilder(); // does not compile

​     objects[0] = new StringBuilder(); // throws an exception java.lang.ArrayStoreException



**- Using Array**



- Se di cerca di accedere ad un indice che è fuori range per l'array si otterrà un eccezione java.lang.ArrayIndexOutOfBuondsException
- La length di un array si riferisce al numero di slot disponibili per l'array e non al suo contenuto
- La length sarà sempre uguale a l'ultimo indice disponibile + 1



**- Sorting**



java.util.Arrays.sort(int[] array) // il metodo .sort() può ordinare qualsiasi tipo di array



Il metodo sort ordina gli array di tipo stringa seguendo queste semplici regole:

- I numeri vengo prima dei caratteri alfabetici
- I caratteri alfabetici maiuscoli vengono prima dei caratteri alfabetici minuscoli.



**- Searching**



java.util.Arrays.binarySearch(int[] array, int search) // allo stesso modo il metodo .binarySarch() può effettuare ricerche in

​                                                       // tutte le tipologie di array.



Il metodo .binarySearch() restituisce dei risultati corretti esclusivamente se l'array passato in input è ordinato, altrimenti il risultato non è prevedibile e sicuramente non è affidabile.



| **Scenario**                                                 | **Result**                                                   |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| L'elemento ricercato viene trovato all'interno dell'array    | viene restituito l'indice in cui si trova l'elemento         |
| L'elemento ricercato non viene trovato all'interno dell'array | viene restituito l'indice in cui si sarebbe dovuto trovare l'elemento secondo l'ordinamento in questa forma: l'indice risultate viene negato e gli viene sottratto 1: -i -1 |



**- Varargs**



Quando un array viene passato come parametro di input in un metodo è possibile usare la sintassi varargs:



public static void main(String arg...){}



Questa sintassi può essere usata solo per l'ultimo parametro di un metodo.



**- Multidimensional Arrays**



In java è possibile usare array multidimensionali, possono essere pensati come un array che contiene degli elementi che a loro volta sono array e cosi via.



int[][] arrayOfArray; 2d array

int arrayOfArray[][]; 2d array

int[] arrayOfArray[]; 2d array

int[] arrayOfArray1[], arrayOfArray2[][]; un 2d array un 3d array



Possono essere creati anche degli array multidimensionali asimmetrici:



int[][] arrayOfArray = {{1,2,3},{3},{5,9}};

int[][] arrayOfArray = new int[3][];

arrayOfArray[0] = new int[3];

arrayOfArray[1] = new int[1];

arrayOfArray[2] = new int[2];





**- Understanding an ArrayList**



Implementa una lista di oggetti ordinata e che consente i duplicati.



**- Creating an ArrayList**



ArrayList arrayList = new ArrayList(); // istanzia un Arraylist vuoto con size di default

ArrayList arrayList = new ArrayList(10); // istanzia un Arraylist vuoto con size = 10, quanto specificato come parametro

ArrayList arrayList = new ArrayList(list2); // crea una copia dell'Arraylist list2.



Gli Arraylist ammettono l'uso dei generics e quindi dell'operatore diamond <> per specificare la tipologia di oggetti che l'arraylist conterrà



ArrayList<String> arrayList = new ArrayList<String>();

ArrayList<String> arrayList = new ArrayList<>();



Inoltre è necessario sapere che la classe ArrayList implementa l'interfaccia List, quindi una variabile di tipo List può contenere un oggetto di tipo ArrayList ma non viceversa.



**- Using an ArrayList**



**Method:**



- **add()**

​     boolean add(E element); // E = generics type indicato se non presente Object

​     void add(int index, E element);



​          Se non viene fatto uso dei generics la lista potrà contenere qualsiasi tipo di oggetto in quanto accetta elementi di tipo Object



​     ArrayList list = new ArrayList();

​     list.add("Hawk");

​     list.add(Boolean.TRUE);

​     System.out.println(list); it prints [hawk, true]



​          Se invece vengono usati i generics l'array list accetterà solamente elementi dello stesso tipo espresso nel operatore diamonds <>



​     ArrayList<String> list = new ArrayList();

​     list.add("Hawk");

​     list.add(Boolean.TRUE); // does not conpile



​          Quando viene utilizzato il metodo add passando come parametro anche l'indice nel quale si vuole aggiungere l'elemento, l'elemento sarà

​          aggiunto nella posizione indicata e gli elementi nelle posizioni successive, se presenti vengo traslati di una posizione.



​     List<String> list = new ArrayList<>();

​     list.add("hawk"); // [hawk]

​     list.add(1, "robin"); // [hawk, robin]

​     list.add(0, "blue joy"); // [blue Joy, hawk, robin]

​     list.add(1, "cardinal"); // [blue Joy, cardinal, hawk, robin]



- **\*remove()***

​     boolean remove(E element); // rimuove il primo elemento corrispondente trovato, ritorna true se rimuove

​                                // l'elemento

​     E remove(int index); // rimuove l'elemento ad un determinato indice, ritorna l'elemento rimosso,

​                          // viene sollevata una ArrayIndexOutOfBuondsException se l'indice non rientra

​                          // nel range dell'ArrayList  



- **\*set()***

​     E set(int index, E element); // Modifica un elemento ad un determinato indice senza variare la size della

​                                  // lista, solleva ArrayIndexOutOfBuondsException se l'indice non rientra nel

​                                  // range della lista



- **\*isEmpty() / size()*** 

​     int isEmpty() // ritorna true se la lista non contiene nessun elemento valorizzato

​     int size() // ritorna il numero di elementi valorizzati all'interno della lista



- **\*clear()***

​     void clear(); // rimuove tutti gli elementi presenti nella lista



- **\*contains()***

​     boolean contains(Object obj); // Restituisce true se all'interno della lista è presente un elemento che

​                                   // corrisponde a quello passato in input, la verifica viene effettuata usando

​                                   // il metodo .equals() sugli elementi della lista



- **\*equals()***

​     boolean equals(Object obj); // Restituisce true se due liste contengono gli stessi elementi (verificare se

​                                 // viene usato il metodo .equals()) nello stesso ordine e quindi implicitamente

​                                 // anche se hanno la stessa size.



**- Wrapper Classes**



Le wrapper class sono tutte *final,* tutte le classi che rappresentano un tipo numerico estendono la classe astratta Number



| **Primitive Type** | **Wrapper Class** | **Example of constructing**                                  |
| ------------------ | ----------------- | ------------------------------------------------------------ |
| boolean            | Boolean           | new Boolean(true)                                            |
| byte               | Byte              | new Byte((byte)1)                                            |
| short              | Short             | new Short((short)1)                                          |
| int                | Integer           | new Integer(1)                                               |
| long               | Long              | new Long(1)                                                  |
| float              | Float             | new Float(1.0) (ha un costruttore che prende in input un double) |
| double             | Double            | new Double(1.0)                                              |
| char               | Character         | new Character('a')                                           |



Tutte le wrapper classes non hanno un costruttore no-argument, tutte le classi numeriche hanno due costruttori, uno che prende come parametro il tipo primitivo di riferimento, mentre l'altro prende come input una stringa, solo la Classe Character ha un solo costruttore che prende come parametro un char.



Il costruttore *new Boolean(String s)* crea un oggetto rappresentante il valore true: se la stringa passata come parametre è equalsIgnoreCase "true"



Ogni classe wrapper ha dei metodi statici specifici che restituiscono i corrispettivi valori primitivi o il wrapper object:



| Wrapper Class | Converting String to Primitive | Converting String to Wrapper Object |
| ------------- | ------------------------------ | ----------------------------------- |
| Boolean       | Boolean.parseBoolean("true")   | Boolean.valueOf("true")             |
| Byte          | Byte.parseByte("1")            | Byte.valueOf("1")                   |
| Short         | Short.parseShort("1")          | Short.valueOf("1")                  |
| Integer       | Integer.parseInt("1")          | Integer.valueOf("1")                |
| Float         | Float.parseFloat("1.0")        | Float.valueOf("1.0")                |
| Double        | Double.parseDouble("1.0")      | Double.valueOf("1.0")               |
| Long          | Long.parseLong("1")            | Long.valueOf("1.0")                 |
| Character     | none                           | none                                |



I metodi parse e valueOf sono sempre statici.



Le classi implementano il metodo equals, quindi verificano l'uguaglianza del loro stato e non delle reference dell'oggetto



Le wrapper class implementano il metodo equals, prende come parametro un Object, ma restituisce true se il parametro non è null, se i due oggetti a confronto sono delle stesso tipo ed i valori che rappresentano sono uguali



![img](https://www.evernote.com/shard/s62/res/f9644223-0034-4444-9eaa-5b4440fa1353/Immagine.png)



**- Autoboxing**



Java in automatico converte i tipi primitivi nelle rispettive Wrapper Class e viceversa:



List<Double> weights = new ArrayList<>();

weights.add(50.0); // il metodo .add vuole in input un Double

weights.add(new Double(60.0);

weights.remove(50.0);

double = weights.get(0); // java in automatico converte il valore Double restituito dal metodo in un double



E' necessario fare attenzione a due casistiche precise quando si lavora con l'auto-boxing:



- se si tenta di fare auto boxing di un valore null verrà sollevata una NullPointerException
- nel caso di invocazione di un metodo che vuole in input un primitivo in caso di ambiguità la priorità sarà data alla tipologia di input del parametro del metodo



​     List<Integer> list = ArrayList<>();

​     list.add(1);

​     list.add(2);

​     list.remove(1); // non viene effettuato l'autoboxing e viene richiamato il metodo .remove(int index)

​     System.out.println(list); // int prints [1]

​     

- Se si tenta di verificare l'uguaglianza tra due istanze di wrapper class non viene applicato l'autoboxing, viene applicato solo nel caso uno dei due operatori è un tipo primitivo
- Se si applica un qualsiasi operatore matematico a due operandi che sono due istanze di wrapper class, l'auto-boxing viene applicato e l'operazione va a buon fine



new Integer(1) == new Integer(1) // false non viene applicato l'auto-boxing e viene verificata l'uguaglianza tra le reference



int r = new Integer(1) + new Integer(1) // r = 2, viene applicato l'auto-boxing ed eseguita l'operazione





**-  Converting Beetween array and List**



E' possibile convertire una List in un array e viceversa:



List<String> list = new ArrayList<>();

list.add("1");

list.add("2");

Object[] arrayObj = list.toArray(); // di default il metodo .toArray() restituisce un Object[]

String[] arrayStr = list.toArray(new String[0]); // è possibile specificare come parametro il tipo di array che si vuole creare

​                                                 // impostando la dimensione dell'array a 0 viene creato un array della stessa 

​                                                 // dimensione della List, se si specifica una dimensione diversa verrà creato

​                                                 // un array dalle dimensione specificata, se non è sufficiente viene creato

​                                                 // un nuovo array di dimensione sufficiente (da verificare)



Per convertire un array in una Lista si usa il metodo Arrays.asList(), è necessario far attenzione al fatto che la lista restituita è legata all'array che l'ha generata ed ha dimensione fissa, non è possibile usare i metodi .add() e .remove(). Se viene modificato un elemento all'interno dell'array viene modificato anche nella List e viceversa.

La tipologia di lista restituita dal metodo sarà fixed-size backed list.



String[] array = { "hawk", "robin" };

List<String> list = Arrays.asList(array);

System.out.println(list.size());

list.set(1,"test"); [hawk, test]

array[0] = "new"; [new, test]

for (String b : array) System.out.print(b + " "); it prints: new test

list.remomve(1); // throws UnsupportedOperationException



**- Sorting**



Collections.sort(list); // effettua l'ordinamento degli elementi seguendo le viste per gli array





**- Working with Dates and Times**



**- Creating Dates and Times**



In java 8 è possibile trattare le Date e i Time con o senza riferimento al TimeZone, per l'esame di certificazione è richiesta esclusivamente la conoscenza delle classi che trattano Date e Time locali.



Tutte le principali classi inerenti si trovano all'interno del package: *java.time.\**



Ci sono tre classi principali:

- LocalDate - gestisce esclusivamente la data e non l'orario
- LocalTime - gestisce esclusivamente l'orario e non la data
- LocalDateTime gestisce sia la data che l'orario



tutte le classi elencate hanno un costruttore privato, quindi è possibile creare una nuova istanza solamente usando i metodi statici:



*- now()* restituisce un oggetto con orario e/o data corrente

\- *of(...)* restituisce un oggetto con orario e/o data secondo i parametri passati in input, ci sono molte combinazioni da verificare con le API.





LocalDate.of(int year, int month, int dayOfMonth);



LocalTime.of(int hour, int minute);

LocalTime.of(int hour, int minute, int second);

LocalTime.of(int hour, int minute, int second, nanos);



LocalDateTime.of(int year, int month, int dayOfMonth, int hour, int minute, int second, int nanos); 

// molte variabili possibili

LocalDateTime.of(LocalDate date, LocalTime time);



Attenzione se vengono passati dei parametri non validi per il contesto data o orario verrà sollevata un eccezione:



LocalDate date = LocalDate.of(2015,1,32); // it throws an java.time.DateTimeException



Da notare che nelle nuove implementazioni per java 8 i mesi non partono più dall'indice 0 ma bensì dall'indice 1, quindi:



Month.JANUARY // vale 1



Inoltre nelle classi LocalTime e LocalDateTime vengono trattati i nanoseconds (da approfondire)



**- Manipulating Dates and Times**



Le classi appena viste sono tutte immutabili, come le stringhe i loro metodi non ne cambiano lo stato.



Sono presenti diversi metodi che consentono di aggiungere o sottrarre valori ad una data o ad un orario:



LocalDate date = LocalDate.of(2014, Month.JANUARY, 20);

date = date.plusDays(2);

date = date.plusWeeks(1);

date = date.plusMonths(1); // setta la data a 2014-02-28 java sa che non esiste il 29/02

date = date.plusYears(5);



LocalDate date = LocalDate.of(2020, Month.JANUARY, 20);

LocalTime time = LocalTime.of(5, 15);

LocalDateTime = dateTime = LocalDateTime.of(date, time);

dateTime = dateTime.minusDays(1);

dateTime = dateTime.minusHours(10);

dateTime = dateTime.minusSeconds(30); // il dateTime.toString() solo ora restituirà anche il valore dei secondi, quando questi

​                                      // pari a zero non vengono restituiti in quanto non usati



I metodi appena visti ammettono, come per le stringhe le invocazioni a catena, molto utili per scrivere meno righe di codice.



I possibili trick che si possono trovare durante l'esame sono i segenti:



LocalDate date = LocalDate.of(2016, 1, 1);

date.plusMonths(1);

System.out.println(date); // it prints 2016/1/1 il risultato dell'invocazione del metodo non è stato assegnato



LocalDate date = LocalDate.of(2016, 1, 1);

date.plusMinutes(10); // it does not compile la classe LocalDate non tratta i minuti come la classe LocalDate non tratta i

​                      // i giorni



**- Working with Periods**



E' possibile convertire le classi LocalDate e LocalDateTime a valori di tipo long:

- LocalDate ha un metodo non statico *.toEpochDay()* che restituisce il numero di giorni trascorsi dal 1/1/1970
- LocalDateTime ha un metodo non statico *.toEpochTime()* che restituisce il numero di secondi trascorsi dal 1/1/1970T00.00
- LocaTime non ha metodi di questo tipo in quanto non avrebbero senso



La classe *Period* definisce un periodo di tempo arbitrario, questo può essere poi aggiunto o sottratto ad una LocalDate o LocalDateTime.



Period period1 = Period.ofYears(1);

Period period2 = Period.ofMonths(1);

Period period3 = Period.ofWeeks(3);

Period period4 = Period.ofDays(2);

Period period5 = Period.of(1,0,7);



LocalDate date = LocalDate.of(2016, Month.JANUARY, 1);

date.plus(period1);

 

Attenzione i metodi di creazione di un Period non possono essere invocati a catena!



Ad una classe LocalTime non posso aggiungere un Period, per ciò che concerne gli orari esiste la classe Duration che segue le stesse logiche di Period ma per gli orari.



**- Formatting Dates and Times**



Per formattare le date in java 8 è necessario usare la classe:



*java.time.format.DateTimeFormatter*



questa mette a disposizione diversi formati standard oppure è possibile selezionarne di diversi.



*java.time.format.DateTimeFormatter.ISO_LOCAL_TIME*

*java.time.format.DateTimeFormatter.ISO_LOCAL_DATE_TIME*

*java.time.format.DateTimeFormatter.ISO_LOCAL_DATE*



Per la formattazione di una data è possibile usare due vie:

- usare il metodo

   

  .format

   

  appartenente alla classe

   

  DateTimeFormatter

   

  il metodo è non-statico quindi è necessario avere un'istanza della classe, ottenibile attraverso principalmente 4 metodi statici:

  - *.ofLocalizedDateTime()*
  - *.ofLocalizedDate()*
  - *.ofLocalizedTime()*
  - *.ofPattern(String patterrn)*

- usare il metodo non-statico *.format()* appartenenti alle classi date *LocalDateTime, LocalDate, LocalTime.*



​        LocalDateTime dateTime = LocalDateTime.now();

​        LocalDate date = LocalDate.now();

​        LocalTime time = LocalTime.now();



​        DateTimeFormatter dateTimeFormatter = DateTimeFormatter.ofLocalizedDateTime(FormatStyle.MEDIUM);

​        DateTimeFormatter dateformatter = DateTimeFormatter.ofLocalizedDate(FormatStyle.SHORT);

​        DateTimeFormatter timeFormatter = DateTimeFormatter.ofLocalizedTime(FormatStyle.MEDIUM);



​        System.out.println(dateTime.format(dateformatter));

​        System.out.println(date.format(dateformatter));

​        System.out.println(time.format(timeFormatter));



​        System.out.println(dateformatter.format(dateTime));

​        System.out.println(dateformatter.format(date));

​        System.out.println(timeFormatter.format(time));



​        System.out.println(dateTime.format(dateTimeFormatter));

​        System.out.println(date.format(dateTimeFormatter)); // throws java.time.temporal.UnsupportedTemporalTypeException

​        System.out.println(time.format(dateTimeFormatter)); // throws java.time.temporal.UnsupportedTemporalTypeException

 

Attenzione! : quando si usa *DateTimeFormatter.ofLocalizedDateTime()*  è possibile formattare esclusivamente oggetti di tipo *LocalDateTime.*



**- Parsing Date and Times**



DateTimeFormatter f = DateTimeFaormatter.ofPattern("MM dd yyyy");

LocalDate date = LocalDate.parse("01 02 2015", f);

LocalTime time = LocalTime.parse("11:22");