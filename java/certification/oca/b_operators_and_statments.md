# Operators and Statments



#### Java Operators

Esistono tre tipologie di operatori:

- unary
- binary
- ternary

la loro tipologia dipende dal numero di operandi su cui lavora l'operatore.

L'ordine di esecuzione di un'espressione dipende dall'ordine di precedenza degli operatori che la compongo:

```java
int y = 4;
double x = 3 + 2 \* --y;

x = 3 + 2 \* 3
x = 3 + 6
x = 9

```

nel caso di esempio appena espresso l'operatore pre-decrement ha una precedenza più alta rispetto agli altri operatori, per questo viene valutato prima degli altri. Nel caso in cui gli operatori presenti nell'espressione hanno lo stesso livello di precedenza vengo valutati in ordine da sinistra a desta. Inoltre l'ordine di esecuzione di un'espressione può essere alterato dall'uso delle parentesi tonde.



| Post-unary operator (increment, decrement) | expression++, expression--                      |
| ------------------------------------------ | ----------------------------------------------- |
| Pre-unary operator (increment, decrement)  | ++expression, --expression                      |
| Other unary operator                       | +, -, !                                         |
| Multiplication / Division / Modulus        | *, /, %                                         |
| Addition / Subtraction                     | +, -                                            |
| Relation operators                         | <, >, <=, >=                                    |
| Equal to / Not equal to                    | ==, !=                                          |
| Logical operators                          | &, \|, ^                                        |
| Short-circuit logical operators            | &&, \|\|                                        |
| Ternary operator                           | boolean expression ? expresion 1 : expression 2 |
| Assignment operator                        | =, +=, -=                                       |



Gli operatori riportati nella tabella appena sopra, sono un subset degli operatori presenti in java, il subset richiesto per l'esame di certificazione.

E' importante ricordare che non tutti gli operatori possono essere usati su determinate tipologie di variabili. (Da approfondire sulle specifiche)



#### Binary Arithmetic Operators

\- Gli operatori aritmetici possono essere applicati a tutti i tipi primitivi java fatta eccezione del tipo boolean.

Mentre al tipo stringa possono essere applicati esclusivamente gli operatori + e +=, usati per la concatenazione di stringhe



\- L'operatore % modulo restituisce il resto di un'operazione di divisione il suo valore è sempre compreso tra 0 e (y-1) dove y è il divisore.

L'operatore modulo si applica anche a dividendi negativi in questo caso il suo valore risultante è sempre compreso tra (-y + 1) e 0 dove y è il divisore.



#### Numeric Promotion

L'esecuzione di un espressione e dei singoli operatori che la contengono, segue delle precise regole di promozione dei tipi di operandi:



1. nel calcolo di un operatore binario se gli operandi sono di tipologia diversa l'operando di tipologia inferiore viene promosso alla stessa tipologia dell'operando con tipologia superiore, prima che venga applicato l'operatore
2. nel calcolo di un operatore binario se un operando è integrale e l'altro decimale, l'operando integrale viene automaticamente promosso a decimale, prima che venga applicato l'operatore
3. gli operandi di tipo byte, short, char se coinvolti in un espressione binaria vengono promossi automaticamente a int, prima che venga applicato l'operatore, anche se nessuno degli operandi coinvolti nell'espressione è di tipo int. Questa regola non si applica agli operatori unari
4. il tipo di dato restituito da un espressione è sempre uguale al tipo di dato superiore e quindi uguale alla maggiore promozione.



```java
int x = 1;

long y = 33;

*\*exp:** x * y
```



la variabile x viene promossa a long e il risultato dell'espressione sarà di tipo long



*double x = 39.21;*

*float y = 45.15F; //ATTENZIONE ALLA 'F' FINALE*

**\*exp:** x * y*



la variabile y viene promossa a double e il risultato dell'espressione sarà di tipo double



*short x = 10;*

*short y = 2;*

**\*exp:** x * y*



le variabili x e y vengono promosse a int ed il risultato dell'espressione sarà di tipo int



*short x = 10;*

*float y = 1.14F;*

*double z = 5.875;*

**\*exp:** x * y / z*



la variabile x viene promossa da prima a int poi a float e il risultato dell'espressione x * y sarà di tipo float, questo poi viene promosso a double per essere calcolato come operando dell'espressione xy / z, il risultato dell'espressione sarà di tipo double.



*char x = 0;*

**\*exp:** x++*



il valore restituito dall'espressione rimane di tipo char, come detto in precedenza agli operatori unari non si applica a regola di promozione ad int dei tipi byte, short, char.



**- Unary Operator**

| +    | indica che un numero è positivo, anche se in java se non è indicato il segno di default il valore è positivo |
| ---- | ------------------------------------------------------------ |
| -    | Indica che un valore è negativo, oppure nega un'espressione  |
| ++   | incrementa il valore di 1                                    |
| --   | decrementa il valore di 1                                    |
| !    | inverte il valore logico di un boolean. non è applicabile a valori numerici, ma esclusivamente a dati di tipo boolean |



Gli operatori binari si applicano ad un solo operando.



**- Logical  complement and negation operators**



il logical complement operator ! inverte il valore logico di variabili o espressioni regolari, può essere applicato solo a valori booleani.



*boolean x = true;*

*x = !x; // x vale false*



mentre il negation operator - inverte il segno di un espressione numerica, può essere applicato esclusivamente a variabili o espressioni di tipo numerico.



*double d = 1.345;*

*d = -d; // d vale -1.345*



**- Increment and decrement operator**



Gli operatori increment e decrement ++, --, possono essere applicati esclusivamente a operandi di tipo numerico, hanno la più alta precedenza di valutazione e possono essere post o pre a secondo della loro posizione rispetto l'operando.



Per processare un espressione che contiene questi operatori è importante valutarli prima tutti quanti e poi procedere con le operazioni successive.



*int x = 3;*

*int y = ++x \* 5 / x-- + --x;*

**\*exp:** y = 4 * 5 / 4 + 3;*

​        *y = 4 \* 5 / 4 + 2;*

​        *y = 20 / 4 + 2;*

​        *y = 5 + 2;*

​        *y = 7*



Un caso particolare che ci fa capire come calcolare per bene gli operatore ++,  -- è il seguente:



int x = 4;

x += x + x++ + ++x + x;       

System.out.println(x); //print 24



//Expression

//= 4 + 4 + 4 + 4 + 4

//= 4 + 4 + 4 + 5 + 5 (eseguo ++x)

//= 4 + 4 + 4 + 6 + 6 (eseguo x++, si applica solamente da sinistra verso destra e 

//                     quindi solo per le variabili che seguono l'operatore unario)

//= 8 + 4 + 6 + 6

//= 12 + 6 + 6

//= 18 + 6

//= 24



**- Binary Operators**



**\*- Assignment Operators***



L'assignment operator = assegna alla variabile presente al lato sinistro dell'operatore il valore risultante dalla variabile o espressione presente al lato destro dell'operatore.



Java in automatico promuove il data type risultante dal tipo più piccolo al tipo più grande, ciò vuoldire che posso assegnare il valore di una variabile di tipo int ad una variabile di tipo long. Ma non è vero il contrario, il compilatore java solleva un errore di compilazione se si tenta di assegnare il valore di una variabile con un data type maggiore ad una variabile con data type di dimensione inferiore.



*long x = 1; // compile*

*int x = 1L; // does not compile*



**- Casting primitive value**



Il casting è necessario quando si vuole assegnare un valore con data type di dimensione maggiore ad una variabile con data type di dimensione minore.



*int x = (int)1.0; // compile*



così facendo si istruisce il compilatore a non applicare il suo comportamento di default, tutto questo però ha un costo in quanto c'è una perdita di dati nell'operazione di casting.



- in caso di casting da un data type decimal ad un data type integral viene troncato tutto quello che c'è dopo la virgola
- in caso di casting tra data type integral con dimensioni differenti e con superamento del range del data type di dimensione inferiore, il compilatore ricomincerà il conteggio dal primo valore negativo ammesso per il data type, mentre in caso di superamento del limite negativo del data type il comportamento sarà l'inverso.
  *int x = 2147483647+1; // x vale: -2147483648*
  *int x = -2147483648-1; // x vale: 2147483647*



Esempio:

*int x = (int)12.3453F; //compile x varrà 12.0*



![img](https://www.evernote.com/shard/s62/res/91126724-4f7a-479a-a8f5-8963ca188fa2/Immagine.png)



**- Compound Assignment Operators**



- I compuond assignment operator possono essere usati esclusivamente su variabili che sono state definite in precedenza nel codice, non possono essere usate all'interno della definizione di una variabile
- Possono essere usati per evitare il casting, in quanto effettuano le operazioni di casting in automatico:
  int x = 5;
  long y = 3;
  x = x + y; // does not compile
  x += y; // compile
- I compound assingnment operator possono essere utilizzati anche come nella seguente forma:
  *x = (x=3); // x varrà 3*nell'espressione prima viene assegnato il valore 3 alla variabile x e successivamente viene restituito il valore della variabile 3



**- Relational Operators**





| <    | strettamente minore di   |
| ---- | ------------------------ |
| >    | strettamente maggiore di |
| <=   | minore uguale di         |
| >=   | maggiore uguale di       |





- Possono essere usati solamente con dati primitivi di tipo numerico
- In caso di confronto tra data type di dimensioni diverse seguono le regole di promozione classiche





| a **instance of** b | restituisce true se la reference 'a' punta ad un oggetto appartenente ad una classe, sotto classe, interfaccia uguale a 'b' |
| ------------------- | ------------------------------------------------------------ |
|                     |                                                              |





**- Logical Operators**





| AND - &                | restiruisce true solo se entrambe gli operandi sono true     |
| ---------------------- | ------------------------------------------------------------ |
| OR - \| (inclusive or) | restituisce true solo se almeno uno dei due operandi è true  |
| XOR - ^ (exclusive or) | restituisce true solo se i due operandi hanno valori diversi |



Gli operatori logici possono essere usati sia data type primitivi numerici e booleani.



I logical operator & e | possono essere usati in short-circuit ovvero si raddoppia il simbolo (&&, ||), ciò comporta che se il risultato dell'espressione può essere calcolato solamente con il primo operando, il secondo operando non verrà valutato.



**- Equality Operators**



Gli equality operator possono essere applicati solamente a tre scenari ben precisi:



1. Comparare due tipi primitivi numerici, le espressioni di comparazione seguono le regole di promozione classiche
2. Comparare due tipi booleani
3. Comparare 2 oggetti compresi null e stringhe, se vengono comparati due oggetti di classi diversa, il compilatore solleverà un errore
4. Non possono essere comparati tipi non omogenei.



Inoltre è necessario fare attenzione: la comparazione tra oggetti viene eseguita tra i riferimenti agli oggetti quindi ciò che viene comparato è il valore della reference e non l'oggetto.



Nel caso di Wrapper Type, auto-boxing viene applicato solamente se uno dei due operandi è un tipo primitivo, altrimenti viene verificata uguaglianza tra il valore delle reference.



Integer i1 = 2;

Integer i2 = 2;

Integer i3 = new Integer(2);

Byte i4 = 2;

int i4 = 2



boolean r = i1 == i2; // true

i1 == i3; // false

i1 == i4; // true

i1 == i4; // does not compile - Il compilatore è in grado di accorgersi che le due variabili puntano a classi diverse e quindi        // non potranno mai avere lo stesso indirizzo di memoria e quindi non potranno mai essere uguali





**- Java Statment**



**- if statment**



You cannot have break or continue in an 'if' or 'else' block without being inside a loop. Note that the problem statement mentions, "...occuring by themselves". This implies that the given statement is not wrapped within any other block.

Note: break with a label is possible in an if/else statement without a loop:

  label: if(true){

  System.out.println("break label");

  break label; //this is valid

  }



**- Ternary Operator**



- Un ternary operator può restituire un risultato avente data type differente a seconda di quale espressione viene eseguita, è un comportamento ammesso e previsto dal compilatore, ma è necessario fare attenzione alla variabile di assegnazione del risultato:
  *System.out.print( (y > 5) ? (2 \* Y) : (3 * y) ); // compileint x =* *(y > 5) ? 9 : "Horse"; // does not compile*
- In un ternary operator viene eseguita una sola espressione tra le due possibili



![img](https://www.evernote.com/shard/s62/res/bd763d0b-0e83-4a1d-be0b-6aae38f28496/Immagine.png)



**- Switch Statment**



\- data type supported

- byte / Byte
- short / Short
- char / Char
- int / Integer
- String
- enum



\- compile time Constant Values 



- Tutti i valore dei case devono essere dello stesso tipo dello switch value
- I valori dei case possono essere esclusivamente di tre tipologie:
  - literal
  - enum
  - final constant (per final constant si intende una variabile dichiarata come final ed inizializzata al momento della sua dichiarazione)
- I case ed il default non devono seguire nessun ordine particolare, a meno che non ci siano necessità relative al flusso logico del programma
- Se il case non viene terminato da un break o un return il flusso di esecuzione continuerà anche nei case successivi, fino a quando non incontra un break o un return o arriva alla fine dello switch. Questo però avviene solamente se il flusso entra in uno dei case o nel default e questi non sono terminati da break o return.



Attenzione lo scope di uno statment switch è unico all'interno delle parentesi {}, ciò vuol dire che una variabile locale dichiarata in un case è accessibile anche dagli altri case successivi.



public class Switcher{



   public static void main(String[] args){

​       switch(Integer.parseInt(args[1]))

​       {

​          case 0 :

​             boolean b = false;

​             break;



​          case 1 :

​             b = true; // is valid

​             break;

​       }



​       if(b) System.out.println(args[2]); // is not valid

   }

}



**- while vs do while**



- la differenza sostanziale tra i due statment di iterazione è nel fatto che nel while non è garantita l'esecuzione del blocco body del ciclo, mentre nel do while l'esecuzione del blocco body è garantita almeno una volta.
- nel do while deve essere fatta attenzione al ; che è richiesto da sintassi



while(false){ // does not compile error: unreachable statement

​     int x = 3;

}



do {

​     int x = 3;

} while (false); // compile



**- for loop**



Il for loop è composto da quattro sezioni ben definite:

- inizializzazione
- espressione
- update
- body

tralasciando il body le altre tre sezioni sono opzionali, sebbene debba essere sempre presente il ; le sezioni possono essere omesse, senza problemi di compilazione:



*for(;;){*

​     *//body*

*}*



- Le sezioni di inizializzazione e update consentono di avere più elementi al loro interno.
- Le variabili dichiarate all'interno della sezione di inizializzazione devono essere tutte dello stesso tipo, seguono le regole di dichiarazione multipla di variabili, il loro scope termina al termine del body del for.
- E' possibile non dichiarare variabili ma semplicemente utilizzarle della variabili dichiarate in precedenza, inizializiandole o assegnadogli un nuovo valore.



Esempi da tenere in considerazione:



for(;;){ // compile

​     //body

}



int x = 0;

for( long y = 0, z = 4 ; x < 5 && y < 10 ; x++, y++ ){ // compile

​     //body

}



int x = 0;

for ( long y = 0, x = 4 ; x < 5 && y < 10 ; x++, y++) { // does not compile

​     //body

}



int x = 0;

long y = 0;

for ( y = 0, x = 4 ; x < 5 && y < 10 ; x++, y++) { //compile

​     //body

}



for ( long y = 0, int x = 0 ; x < 5, y < 5 ; x++, y++) { //does not compile

​     //body

}



for ( long y = 0, x = 0 ; y < 5, x < 5 ; x++, y++ ) {

​     //body

}

System.out.println(x);



for(;false;) int x = 3; // does not compile error: unreachable statement



**- for each**



- Consente l'iterazione su array o oggetti che implementano l'interfaccia java.lang.Iterable
- Se la classe dell'oggetto che conterrà l'item di iterazione non corrisponde con la classe degli oggetti contenuti nell'array o nella lista viene restituito un errore di compilazione, o in casi specifici un eccezione a runtime.



**- Option label**



Usate per consentire di modificare il flusso di un programma attraverso le istruzioni break e continue:



OPTION_LABEL: for(;;){}



- i loro identificativi seguono le regole standard
- la nomenclatura standard java prevede che siano in maiuscolo e le parole vengano separate da _
- una label è "visibile" solamente all'interno del suo scope, che è definito dal singolo statment abbinato alla label, quindi ad esempio se lo statment è un for la label è visibile solamente all'interno dello scope del for. Esempio:





void crazyLoop(){

​     int c = 0;

​     JACK: while (c < 8){

​          JILL: System.out.println(c);

​          if (c > 3) break JILL; else c++;  // does not compile: error: undefined label: JILL          

​     }

}

 

/* ------------------- */

 

void crazyLoop(){

​     int c = 0;

​     JACK: while (c < 8){

​          JILL: {

​               System.out.println(c);

​               if (c > 3) break JILL; else c++; // compile - la label JILL definisce un scope più ampio

​          }

​     }

}     





| statment         | previsto | continue | break                                                        |
| ---------------- | -------- | -------- | ------------------------------------------------------------ |
| if               | si       | no       | si (ma esclusivamente associato ad una label o all'interno di un loop o di uno switch) |
| while / do while | si       | si       | si                                                           |
| for / for each   | si       | si       | si                                                           |
| swhitch          | si       | no       | si                                                           |



**- break**



L'istruzione break consente di interrompere l'esecuzione di un cliclo (while / do while / for) o di uno switch.



Accetta come parametro opzionale l'identificativo di una option label:

​     *break OPTION_LABEL;*



Se non è presente alcun identificativo di option label l'istruzione break interrompe l'esecuzione dello statment in cui si trova tornando al controllo più vicino a se.



Se è presente l'identificativo di option label l'istruzione break interrompe l'esecuzione non solo dello statement in cui si trova ma arriva fino allo statement a cui appartiene la option label.



**- continue**



L'istruzione continue interrompe l'esecuzione di una singola iterazione di un ciclo, riportando il controllo all'espressione booleana di verifica del ciclo.



Segue le stesse regole dell'istruzione break per quanto concerne le option label.