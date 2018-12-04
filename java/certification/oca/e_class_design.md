# Class Design



**Introducing class Inheritance**

![mappa_concettuale_class_design](/home/dev/notes/resources/mappa_concettuale_class_design.png)



Una classe java può estendere altre classi:

- può estendere una sola classe
- ma può essere estesa da più classi
- può implementare 0..n interfacce



Una classe sub-class è di dimensione più grandi rispetto alla sua super-class in quanto include tutti i membri della super-class, anche quando questi non sono direttamente accessibili perchè sono private o default access modifier. Questo è molto importante soprattutto per le variabili di istanza.



**Appliyng Class Access Modifiers**



Una classe "normale" può essere definita con i seguenti modificatori di accesso:

- public
- default



I modificatori di accesso:

- protected
- private

possono essere applicati solamente a delle inner class



La stessa regola vale per le interfacce.



**Creating Java Oblects**



In java ogni classe estende java.lang.Object, ogni qualvolta viene creato un oggetto che non estende nessuna classe il compilatore in automatico aggiunge alla classe l'estensione della classe java.lang.Object.



Di fatto la super-class di tutte le classi java è proprio Object, di conseguenza Object è l'unica classe che non estende nessuna classe.



**Defining Constructors**



In java il primo statment di un qualsiasi costruttore di una classe, sia dichiarato dallo sviluppatore sia quello di defualt fornito dall compilatore, deve iniziare con invocazione di un altro costruttore presente all'interno della classe, con l'istruzione *this()*  o con l'invocazione di un costruttore della sua super-class, attraverso l'uso dell'istruzione *super().*



Attraverso l'overloading può essere richiamato uno qualsiasi dei costruttori presenti nella classe o nella sua super-classe.



Se i costruttori della super-class prevedono dei parametri, la chiamata al costruttore della super-class dovrà prevedere anch'esso dei parametri.



**Constructors Rules**



1. Il primo statement di un costruttore deve sempre essere una chiamata ad un altro costruttore interno alla classe con *this()* o di una sua super-classe con *super()*
2. L'istruzione *super()* può essere usata solo come primo statement di un costruttore, in qualsiasi altra posizione causa errori di compilazione - (Attenzione anche l'istruzione *this(),* può essere esclusivamente usato come primo statement di un costruttore)
3. Se non è presente l'istruzione *super()* all'interno di un costruttore, il compilatore in automatico inserisce l'istruzione *super()* (default no-argument) come primo statement del costruttore
4. Se la super-class non ha un costruttore no-argument e la sub-class non definisce alcun costruttore, il compilatore inserirà automaticamente un costruttore di default, ma solleverà un errore in compilazione in quanto non sarà in grado di usare l'istruzione *super(),* per richiamare il costruttore no-argument della super-class
5. Se la super-class non ha un costruttore no-argument, la sub-class dovrà necessariamente definire in maniera esplicita un costruttore che usi l'istruzione super(arguments...) per invocare uno dei costruttori della sua super-class



Nota:

Il compilatore si accorge e solleva errore se si creano chiamate ricorsive di costruttori attraverso l'istruzione *this()*



**Calling constructor**



A runtime, viene sempre richiamato prima il costruttore della super-class e poi in successione i costruttori delle sub-classes.



**Calling Inherited Class Members**



Una sub-class può avere accesso a tutti i membri *public* o *protected* della sua super-class, se le due classi si trovano nello stesso package, la sub-class avrà accesso anche a tutti i membri con modificatore di accesso di default della super class.



La sub-class può accedere invece in maniera indiretta ai membri privati, ad esempio attraverso metodi get implementati dalla super-class



E' possibile accedere ai membri di istanza di una classe anche attraverso la keyword *this,* attraverso questa è possibile accedere anche ai membri ereditati dalla super-class.

Con la keyword *super* una sub-class può accedere ai membri si una sua super-class, ma ovviamente non può accedere ai propri membri.



Nota:



E' necessario non confondere mai le keywords this - this() e super - super() che sono totalmente differenti



La keyword *super* può essere usata sia nelle classi che nelle interfacce, ma per far riferimento ad un membro di un interfaccia è necessario specificare anche il nome dell'interfacca: *Interface.super.member*



**Inhereting Methods**



**Overriding Methods**



Regole ovverride metodi public, protected o default:



1. I metodi devono avere la stessa signature, stesso nome e stesso elenco dei parametri
2. Il metodo dichiarato nella sub-class deve avere modificatore di accesso uguale o che garantisca una visibilità maggiore
3. Un return type covariant, ovvero deve restituire lo stesso type o una sua sub-class, in caso il return type è un primitivo il metodo che fa overriding deve restituire esattamente lo stesso tipo
4. Può sollevare eccezioni che siano delle sub-class di quelle sollevate dal metodo su cui fa override o può eliminare le eccezioni sollevate dal metodo su cui fa ovveride, non può sollevare nuove eccezioni, o eccezioni che non siano delle sub-classes di quelle sollevate. 



**Overriding Private Methods**



Un metodo privato non è accessibile da una sub-class, c'ho vuol dire che se la sub-class reimplementa un metodo con la stessa signature di un metodo di una sua super-class non sta facendo overriding del metodo, i due metodi saranno del tutto non correlati, quindi tutte le regole viste in precedenza non si applicano nel caso di metodi privati.



**Hidding Static Methods**



Ha le stesse regole dell'ovveride ma questo si applica a metodi statici e per questo motivo aggiunge una quinta regola:



1. I metodi devono avere la stessa signature, stesso nome e stesso elenco dei parametri
2. Il metodo dichiarato nella sub-class deve avere modificatore di accesso uguale o che garantisca una visibilità maggiore
3. Un return type covariant, ovvero deve restituire lo stesso type o una sua sub-class
4. Può sollevare eccezioni che siano delle sub-class di quelle sollevate dal metodo su cui fa override o può eliminare le eccezioni sollevate dal metodo su cui fa ovveride, non può sollevare nuove eccezioni, o eccezioni che non siano delle sub-classes di quelle sollevate. 
5. Se il metodo nella super-class è static deve esserlo anche nella sub-class, altrimenti viene sollevato un errore in fase di compilazione



**Overriding vs. Hiding Methods**



Esiste una differenza sostanziale tra l'overriding e hiding di un metodo:



- Overriding: il metodo viene rimpiazzato dalla nuova implementazione sia per la super-class che per la sub-class, quindi viene richiamato sempre il metodo della sub-class, anche quando l'invocazione del metodo viene eseguita all'interno della super-class
- Hiding: il metodo viene solamente rimpiazzato all'interno della sub-class, quindi invocazioni del metodo effettuate all'interno della super class, invocheranno il metodo all'interno della super-class e non quello implementato all'interno della sub-class



Esempio Hiding:



public class Marsupial{

​     public static boolean isBiped(){

​          return false;

​     }

​     public void getMarsupialDesc(){

​          System.out.println("result: " + isBiped());

​     }

}



public class Kangaroo extends Marsupial{

​     public static boolean isBiped(){

​          return true;

​     }

​     public void getKangarooDesc(){

​          System.out.println("result: " + isBiped());

​     }     

}



public static void main(String[] args){

​     Kangaroo k = new Kangaroo();

​     k.getMaursupialDesc(); // prints false 

​     k.getKangarooDesc();   // prints true

}



Esempio Override:



public class Marsupial{

​     public boolean isBiped(){

​          return false;

​     }

​     public void getMarsupialDesc(){

​          System.out.println("result: " + isBiped());

​     }

}



public class Kangaroo extends Marsupial{

​     public boolean isBiped(){

​          return true;

​     }

​     public void getKangarooDesc(){

​          System.out.println("result: " + isBiped());

​     }     

}



public static void main(String[] args){

​     Kangaroo k = new Kangaroo();

​     k.getMaursupialDesc(); // prints true 

​     k.getKangarooDesc();   // prints true

}



**Creating final methods**



Un metodo *final* non potrà mai essere reimplementato da una sub-class, ne che si tratti di Overriding ne che si tratti di hiding.





**Inheriting Variables**



In java le variabili, sia di istanza che di classe, possono essere solamente nascoste e non sovrascritte, come avviene per i metodi statici, le regole sono le stesse, la sub-class avrà due distinte copie della variabile, se il codice che accede alla variabile si trova all'interno della super-class verrà restituita la copia relativa alla super-class, se il codice che accede alla variabile si trova all'interno della sub-class verrà restituita la copia relativa alla sub-class, da notare che la sub-class può accedere alla copia della super-class usando l'istruzione *super.*



class Animal {



​     public int length = 2;



​     public int getAnimalLength(){

​          return length;

​     }

}



public class JellyFish extends Animal {



​     public int length = 4;



​     public int getJellyFishLength(){

​          return length;

​     }



​     public static void main(String[] args){

​        JellyFish j = new JellyFish();

​        Animal a = new JellyFish();

​        System.out.println(j.getAnimalLength()); // prints 2

​        System.out.println(j.getJellyFishLength()); // prints 4



​        System.out.println(j.length); // prints 4

​        System.out.println(a.length); // prints 2

​     }



}



**Abstract Class**



Le *abstract class:*



- possono dichiarare membri non abstract
- possono non dichiarare metodi abstract, ma i metodi abstract possono essere dichiarati esclusivamente all'interno di abstract class
- non possono essere dichiarate come final il compilatore solleva un errore
- i meodi abstract non possono essere ne private ne final, il compilatore solleva un errore



**Creating Concrete Class**



Una classe concreta è la prima classe non astratta che estende una classe astratta, questa deve implementare tutti i metodi astratti della sua super-class. Questa a sua volta può essere estesa da altre classi.



La prima classe concreta deve implementare tutti i metodi astratti della classe astratta che estende, altrimenti verrà sollevato un errore di compilazione.



**Extending Abstract Class**



Una classe astratta può essere estesa da una classe che a sua volta è astratta, la sub-class astratta eredita tutti i metodi astratti e non della super-class, con la differenza che può non fornire una implementazione concreta dei metodi astratti della super-class.



La classe che estende la sub-class estesa a sua volta dovrà fornire l'implementazione concreta dei metodi astratti sia delle sue super-classes da cui discende, a meno che delle classi astratte intermendie non abbiano già fornito delle implementazioni concrete dei metodi astratti.



**Regole di riepilogo**



Una classe astratta:



- non può essere inizializzata direttamente
- può definire un numero qualsiasi di metodi astratti, può anche non definirne nessuno
- non può essere final o private
- che estende una super-class astratta eredita tutti i suoi metodi astratti
- la prima classe concreta che estende la classe astratta deve fornire tutti i metodi astratti che eridita



Un metodo astratto:



- può essere definito esclusivamente in una classe astratta
- non può essere dichiarato come final o private
- non deve avere un corpo
- l'implementazione in una classe concreta di un metodo astratto ereditato segue le stesse regole dell'overrifing



**Implementing Interface**



**![img](https://www.evernote.com/shard/s62/res/57eab086-576a-45e3-b75d-d0eacf3253e6/Implementing%20Interface.png)**



Un interfaccia:



- può definire una serie di metodi astratti
- costanti
- metodi default
- metodi static



**Defining an Interface**



Un'interfaccia:



- non può essere istanziata direttamente
- può non avere alcun metodo astratto o default
- non può essere final
- tutte le interfacce top-level (non inner), devono avere il modificatore di accesso uguale a public o default, altrimenti viene sollevato un errore di compilazione.
- tutti i metodi non *default* o *static* devono avere i modificatori *public* e *abstract*, se presentano uno dei modificatori *private, protected* o *final* verrà sollevato un errore di compilazione, se non viene inserito nessun modificatore, il compilatore in automatico inserirà i modificatori *public abstract*



public interface CanFly{

​     void fly(int speed);

​     abstract void takeOff();

​     public abstract double dive();

}



/* dopo la compilazione diventa */



public interface CanFly{

​     public abstract void fly(int speed);

​     public abstract void takeOff();

​     public abstract double dive();

}





**Inheriting an Interface**



- Un'interfaccia che estende un'altra interfaccia eredita tutti i suoi metodi astratti
- La prima classe concreta che implementa l'interfaccia dovrà fornire un'implementazione di tutti i metodi astratti contenuti dall'interfaccia implementata e tutti i metodi astratti ereditati dall'interfaccia
- Un'interfaccia può estendere più interfacce
- Se una classe astratta implementa un'interfaccia può non fornire un'implementazione concreta dei metodi astratti dell'interfaccia



**Classes, Interfaces, and Keywords**



Un'interfaccia può:



- estendere un'interfaccia



Un'interfaccia non può:



- implementare un'interfaccia
- estendere una classe



Una classe può:



- estendere una classe
- implementare un'iterfaccia



Una classe non può:



- implementare una classe
- estendere un'interfaccia



**Abstract Methods and Multiple Inheritance**



- Nel caso in cui un'interfaccia estende più interfacce che hanno uno o più metodi astratti con lo stesso nome e la stessa lista di parametri, la classe concreta che implementa l'interfaccia fornirà con un solo metodo l'implementazione concreta di tutti i metodi astratti con la stessa signature

- Nel caso in cui un'interfaccia estende più interfacce che hanno uno o più metodi astratti con lo stesso nome ma con parametri diversi, i metodi verranno considerati in overloading e quindi la classe concreta che implementerà l'interfaccia dovrà fornire l'implementazione di tutti i metodi astratti.

- Nel caso in cui un'interfaccia estende più interfacce che hanno uno o più metodi astratti con la stessa signature ma return type differente, il compilatore solleverà un errore, in quanto la casistica non è ammessa, lo stesso per una classe (concreta o astratta) che implementa le stesse due interfacce. Vengono seguite le stesse regole del classico overriding, ovvero è ammesso usare return type covariant, ed sub classes per le eccezioni o rimuovere del tutto le eccezioni.  

  - nel caso di un'interfaccia l'errore di compilazione viene dato sulla dichiarazione dell'interfaccia

  - nel caso di una classe astratta l'errore di compilazione viene dato sulla dichiarazione della classe

  - nel caso di una classe concreta l'errore di compilazione viene dato sui singoli metodi affetti dalla problematica




**Interface Variables**



- Interface variables devono essere *public static final*, se questi modificatori vengono omessi il compilatore lì inserisce in maniera automatica, se vengono usati altri modificatori viene sollevato un errore di compilazione
- Le interface variables devono essere inizializzate contestualmente alla loro dichiarazione



public interface CanSwim {

​     int MAXIMUN_DEPTH = 100;

​     final static boolean UNDERWATER = true;

​     public static final String TYPE = "Submersible"

}



/* dopo la compilazione diviene: */



public interface CanSwim {

​     public static final int MAXIMUN_DEPTH = 100;

​     public static final static boolean UNDERWATER = true;

​     public static final String TYPE = "Submersible"

}



- E' necessario tenere in considerazione le casistiche di ambiguità delle variabili dichiarate con lo stesso nome da più interfacce implementate da un unica classe, di per se questo non causa problemi, viene sollevato un errore di compilazione nel caso in cui nella classe si faccia riferimento alla variabile in maniera ambigua:



interface I1{

   int VALUE = 1;

   void m1();

}

interface I2{

   int VALUE = 2;

   void m1();

}



class TestClass implements I1, I2{ // it compiles - non importa se all'interno delle intefacce ci sono ambiguità

   public void m1() { System.out.println("Hello"); }

   public static void main(String[] args){

​      TestClass tc = new TestClass();

​      ((I1) tc).m1();

​      int x = VALUE; // it does not compile - caso di riferimento ambiguo 

   }

}





**Default Interface Methods**



Un default method:



- può essere presente esclusivamente all'interno di interfacce
- deve avere il modificatore *default* all'interno della sua dichiarazione, e deve avere un corpo
- non può essere ne *static,* ne *final*, ne *abstract*
- è sempre *public,* se non presente il modificatore di accesso nella sua dichiarazione il compilatore inserirà in automatico il modificatore *public*
- non può essere *private* o *protected*, in caso contrario viene sollevato un errore di compilazione



Una classe che implementa un interfaccia che al suo interno ha dei metodi di default può decidere se fare overriding dei metodi di default o usare l'implementazione di default



Le interfacce e le classi astratte che estendono o implementano interfacce che hanno dei metodi di default possono allo stesso modo fare overriding dei metodi di default o usare le loro implementazioni di default, ma inoltre possono ridefinire i metodi come astratti e quindi costringere le proprie classi figlie a fornire un'implementazione per i metodi. L'interfaccia non avrà bisogno di usare il modificatore *abstract* nella ridefinizione del metodo, mentre la classe astratta dovrà usarlo.



**Default Methods and Multiple Inheritance**



Java 8 con l'introduzione dei metodi default ha aperto le porte a la multiple inheritance, ma come gestisce le casistiche di conflitto?



- se una classe sia astratta che concreta implementa più interfacce che al loro interno hanno metodi di default che hanno la stessa signature, il compilatore solleverà un errore
- se la classe che implementa le interfacce aventi metodi di default con signature uguali, fa overriding dei metodi di default, il compilatore saprà quale implementazione del metodo usare e quindi compilerà senza eccezioni.
- Se i due metodi che hanno la stessa signature all'interno delle due interfacce hanno dei return type che non sono covariant, il compilatore solleverà eccezione sia nella definzione della classe o interfaccia che implementa/estende le due interfacce sia quando alle definizione del metodo preposto all'overriding dei metodi di default



**Static Interface Methods**



Sostanzialmente i metodi statici definiti all'interno di interfacce funzionano nella stessa maniera dei metodi statici definiti all'interno di classi, la differenza è che questi non vengono ereditati dalle classi che implementano l'interfaccia.



Inoltre i metodi statici definiti all'interno di interfacce:



- come tutti i metodi di un interfaccia sono sempre *public,* e non possono mai essere *private* o *protected*
- per invocarli è sempre necessario far riferimento al nome dell'interfaccia
- se una classe implementa più di un interfaccia che al suo interno definisce dei metodi statici aventi la stessa signature, il compilatore non incontrerà problemi, in quanto i metodi non vengono ereditari, e ci si può riferire loro esclusivamente attraverso il nome dell'interfaccia.



**Understanding Polymorphism**



In java la reference di un oggetto può essere:

- dello stesso type dell'oggetto
- una super-class dell'oggetto
- una delle interfacce implementate dall'oggetto 



I membri che possono essere acceduti attraverso una reference sono esclusivamente quelli esposti dalla refeerence stessa, non importa a quale oggetto essa si riferisca.



**Object vs. Reference**



1. Il type dell'oggetto definisce il set di proprietà presenti nell'oggetto istanziato in memoria
2. Il type della reference definisce il set di proprietà accedibili



**Casting Objects**



- Il cast non è necessario nel caso in cui si assegna la reference di una sub-class alla reference di una delle sue super-class
- Il cast è necessario nel caso in cui si assegna la reference di una super-class ad una reference di una delle sue sub-classes
- Il compilatore solleva un errore nel caso in cui si cerchi di fare il casting tra reference che non sono correlate
- Anche se il casting non solleva errori di compilazione, perchè corretto, è possibile il verificarsi di eccezioni a runtime (ClassCastException) nel caso in cui si assegni una reference ad un oggetto non correlato



**Virtual Methods**



I metodi virtuali possono essere definiti come quei metodi la cui implementazione non è comosciuta fino al runtime del programma.

In java qualsiasi metodo che non sia *private, final* o *static* è potenzialmente un metodo virtuale.



public class Bird {



​     public String getName(){

​          return "Unknown";

​     }

​     

​     public void displayInfo(){

​          System.out.println("Bird name: " + getName());

​     }

}



public class Peacock extends Bird {

​     

​     public String getName(){

​          return "Peacock"; 

​     }



​     public stattic void main(String[] args){

​          Bird bird = new Peacock();

​          bird.displayInfo(); // it prints: Bird name: Peacock

​     }

}



**Polymorphic Parameters**



Un metodo può avere come parametri interfacce, classi astratte e concrete che sono delle super-class e ricevere come parametri nella sua invocazione istanze di oggetti che implementano le interfacce definite come parametro, o le subclasses che estendono le super-classes definite come parametri.



Questa caratteristica consente la riusabilità del codice, prendere ad esempio le collections.



Sorgente mappa concettuale: 

[![img](https://www.evernote.com/images/file-generic.png)OCA - Mappa Concettuale - Cap...
2.3 KB
](https://www.evernote.com/shard/s62/res/d17686f4-6541-45e5-b221-7c14959086fd/OCA%20-%20Mappa%20Concettuale%20-%20Capitolo%205.xml)