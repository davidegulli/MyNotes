# Exceptions



**Understanding Exceptions**



Le eccezioni consentono la gestione di errori che vengono riscontrati all'interno di un programma java.



- la gestione delle eccezioni può alterare il flusso del programma



**Exception Types**



Le eccezioni possono essere di diversa tipologia, segue schema:



​                              java.lang.Object

​                              java.lang.Throwable

​          java.lang.Exeption               java.lang.Error

​          java.lang.RuntimeException





**Error**

Sono eccezioni fatali sollevate direttamente dalla jvm che inducono la prematura fine dell'esecuzione del programma



**Exception**

Costituiscono il gruppo delle checked exception, ovvero quelle eccezioni che devono essere gestite, tramite try-catch o rilanciate nuovamente tramite throws, altrimenti il compilatore solleva un errore



**RuntimeException**

Le eccezioni più comuni che possono essere gestite, ma non lo richiedono.



**Throwing an Exception**



E' possibile sollevare un eccezione da qualsiasi punto del codice attraverso l'istruzione *throw,* ciò comporta che il chiamante dovrà preoccuparsi di implementare le logiche di gestione dell'eccezione.





| **Type**                     | **How to recognize**                                  | **Okay for program to catch** | **Is program required to handle or declare?** |
| ---------------------------- | ----------------------------------------------------- | ----------------------------- | --------------------------------------------- |
| RuntimeException (unchecked) | Subclass of RuntimeException                          | yes                           | no                                            |
| Exeption (checked)           | Subbìclasses of Exception but not of RunTimeException | yes                           | yes                                           |
| Error                        | Subclass of Error                                     | no                            | no                                            |



E' possibile fare il throw di un eccezione di tipo checked solamente se si è inserita la dichiarazione dei throws nella definizione del metodo, mentre è possibile fare il throw di eccezioni unchecked senza necessità di dichirazione dei throws nella definizione del metodo.



Se viene inserito un blocco catch che gestisce un'eccezione checked che non viene dichiarata da nessuno dei metodi presenti nel try il compilatore solleva un errore di compilazione



**Using a try Statment** 





try {

​     throw new RuntimeException();

} catch(Exception exc) {

​     exc.printStackTrace();

}



- le parentesi graffe sono sempre necessarie anche quando contengono una sola istruzione
- il try deve essere sempre seguito almeno da un'altra clausola (catch - finally)



**Adding Finally Block**



try {

​     throw new RuntimeException();

} catch(Exception exc) {

​     exc.printStackTrace();

} finally {

​     // it is always executed

}



Il blocclo *finally* viene sempre eseguito, sia nel caso non venga sollevata alcuna eccezione nel try, sia che invece venga sollevato un eccezione nel try e venga eseguito il blocco catch.

Se presente il blocco finally il blocco catch diventa opzionale:



try {

​     // it compile

} finally {

​     // it is always executed

}



**Catching Various Types of Exceptions**



E' possibile avere più catch block per gestire più eccezioni nell'esecuzione delle istruzioni presenti in un blocco try.



- in caso di eccezione viene eseguito sempre un solo blocco catch
- il compilatore esamina i cacth nell'ordine in cui appaiono
- è possibile che un blocco catch non sia raggiungibile ed in fase di compilazione viene sollevato un errore, questo avviene se l'ordine delle clausole di catch, una super-class si trova prima di una sub-class



class AnimalOutForAWalk extends RuntimeException {}

class ExhibitClosed extends RuntimeException {}

class ExhibitClosedForLunch extends ExhibitClosed {}



try {

​     seeAnimal();

} catch(AnimalOutForAWalk e) {

​     System.out.printl("try back later");

} catch (ExhibitClosed e) {

​     System.out.printl("not today");

}





try {

​     seeAnimal();

} catch(ExhibitClosedForLunch e) { // sub-class

​     System.out.printl("try back later");

} catch (ExhibitClosed e) { // super-class

​     System.out.printl("not today");

}





try {

​     seeAnimal();

} catch(ExhibitClosed e) { // super-class

​     System.out.printl("try back later");

} catch (ExhibitClosedForLunch e) { // sub-class does not compile

​     System.out.printl("not today");

}



**Throwing a Second Exception**



All'interno di un qualsiasi blocco try / catch / finally è possibile inserire qualsiasi istruzione valida, compresi dei nuovi blocchi try/catch/finally, quindi annidare la gestione delle eccezioni.



E' necessario prestare attenzione ad un caso particolare:



try{

​     throw new RuntimeException();

} catch(RuntimeException e) {

​     throw new RuntimeException(); 

} finally {

​     throw new Exception();

}



L'eccezione che viene sollevata alla fine dell'esecuzione del blocco è Exception, in quanto il blocco finally è l'ultimo ad essere eseguito.



**Recognize Common Exception Types**



Come abbiamo visto esistono tre macro gruppi di eccezioni:



**RuntimeException (unchecked)**



- ArrayIndexOutOfBoundsException
- ArithmeticException
- IllegalArgumentException
- NullPointerException
- ClassCastException
- NumberFormatException
- SecurityException



**Checked Exception**



- IOException
- FileNotFoundException



**Errors**



Eccezioni sollevate direttamente dalla jvm, non dovrebbero essere gestite o dichiarate dagli sviluppatori



- ExceptionInIntitializereError
- StackOverflowError
- NoClassDefFoundError





**Calling Methods That Throw Exceptions**



- Se viene invocato un metodo che dichiara una checked exception, il metodo chiamante dovrà o gestire l'eccezione in un blocco try-catch o dichiarare a sua volta l'eccezione
- Non è possibile getstire un eccezione checked in un metodo try-catch se all'interno del blocco try non ci sono invocazioni a metodi che dichiarano quella specifica eccezione, pena errore in fase di compilaizone



**Subclass**



A questo punto è possibile rivedere le regole dell'overriding relative alle eccezioni:



Un metodo che fa overriding di un metodo della sua super-class



- non può dichiarare nuove eccezioni (checked)
- non può dichiarare eccezioni di tipo "superiore" super-class
- può eliminare la dichiarazione di una o n eccezioni rispetto al metodo della super-class
- le regole per le RuntimeException sono differenti, ad esempio può sollevare nuove eccezioni di tipo RuntimeException, in quanto la dichiarazione e ridondante, non c'è bisogno di dichiarare un'eccezione unchecked



**Printing an Exception**



Ci sono diversi modi per poter stampare un eccezione, i principali sono:

- lasciare a java l'incombenza
- stampare solo il messaggio descrittivo dell'eccezione
- stampare tutto lo stack, ovvero tutti i metodi invocati in maniera annidata fino a quello che effettivamente ha gestito l'eccezione



System.out.println(exc);

System.out.println(exc.getMessage());

exc.printStackTrace();