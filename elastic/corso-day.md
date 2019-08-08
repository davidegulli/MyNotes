## Corso Elastic



**Elastic:**

- Full text search engine
- Lucene based, writeen in java
- Distribuited, (Near) real time, search engine
- Restful, json, http, easy to debug
- Dynamic mapping
- Scalable: form 1 node to  1000 nodes



- High Availabiity
- Rich search feature (
  - Framework interno DSL
- Built in Analitycs 
  - Framework interno per le aggregazioni
- Open Soure (Apache 2.0) Writen by Shay Bannon
- Easy to Install



##### Architecture

**Master Nodes**

- Orchestra lo stato del cluster
- traccia quali nodi sono parte del cluster
- decide quali shards vengono allocati su quali nodi
- se cade il master, uno degli altri cluster viene eletto come nuovo master, a fronte di ciò avviane una fase di resahrding tra i nodi
- E' bene non stressare mai il master

**Coordinator Nodes**

- client che riceve le richeiste

**Data Nodes**

- fa le cose difficili 
- questi contengono gli indici e gli shards
- questi fisicamente effettuano le ricerche e le aggregazioni
- non c'è limite su quanti nodi data possono essere inseriti in un cluster



Quando viene creato un indice questo risiede in 5 shard primari e una replica. Sul singolo nodo elastic va in status yellow perchè non può allocare la replica per i shard

**Client Nodes**

- questi rimpiazzano i master per quanto riguarda le ricerche
- sono un trucco per non uccidere il master
  - I sviluppatori e utenti tendono a fare cattive query
    - queste possono uccidere il master node

**Ingest Node**

- forniscono supporto per ingest pipeline
- questi possono morire senza incidere sul cluster
- sono indipenedenti dai data e master node
- sono ideal per NPL e enrichment pipeline
- un'alternativa è l'utilizzo di logstash, più adatto per grandi modifiche ai dati 

--------------------

**Index**

- é un insieme più o meno omogeneo di documenti
- in un singolo cluster, si possono definire quanti indici si vuole

**Type**

- deprecato dalla 6.0.0
- Dalla 7 in poi il modello di documento si definisce da un attributo del documento, le relazioni tra modelli vengono definiti da un attributo nativo all'interno del documento

**Document**

- unità base dell'informazione che può essere indicizzato
- un documento viene espresso in json

-----------------------

**API REST**

elastic si contatta sempre attraverso API Rest

- usabile in ogni linguaggio grazie a librerie
- le interfacce librerie cambiano raramente
- JSON Based

--------------

**Starting Elastic Search**

./bin/elasticsearch

use -d to run as deamon

./bin/elasticsearch -d -p elastic.pid

NB port: 9200

----------------------

**Static Data vs Time Series**

- data statici non dipendono dal tempo
  - per esempio un catalogo nel quale:
    - ogni prodotto è un document che avrà come attributi le caratteristiche del prodotto
    - i dati cambieranno poco
- time series dipendono dal istante temporale di riferiemento
  - per esempio un file di log nel quale:
    - ogni singola linea è riferita ad un istante temporale



NB: è sconsigliabile avere dei document con più di 2000 attributi sul singolo livello

----------------------

**Elastic Stack Component**

- Vm o Cloud elastic - Deployments
- Logstash (filtering enrichment) o Beats - Input
- Elasticsearch - Store, Search, Analytics
- Kibana - Visualization (Dev Tool, Query, ML, Graph, Allarmistica) Xpack

------------------

**Elastic Structure**

![1548758299729](/home/davide/.config/Typora/typora-user-images/1548758299729.png)



http://localhost:9200 - endpoint rest base

http://localhost:9200/_cat - visualizza gli endpoint di gestione

-------------------------

**Starting Kibana**

``` bash
./bin/kibana
```

http://localhost:5601

**Dev Tool:**

![1548758999401](/home/davide/.config/Typora/typora-user-images/1548758999401.png)



----------------------

**Supported base Types**

- String (text/keywords)
- Boolean
- Date/Datetime
- Numbers
  - Short/Integer/Long/Double
- IP
- Geo Point / Geo Shape

**Supported Advanced Types**

- Object
- Nested
- Array: non ci sono tipi dedicati, ogni campo può contenere uno o più valori

1. Gli array di oggetti non lavorano come ci si aspetta
2. non è possibile fare delle query di un singolo oggetto indipendentemente dagli altri oggetti contenuti nell'array
3. dovrebbe essere usato il nested type piuttosto che l'object type

----------------------

**Automatic Mapping Creation**

consente di indicizzare un documento senza creare uno schema a priori, elastic ne crea uno dinamicamente

- suggested/explicit mapping
  - fast start
- Genral usable mappings for new data
- just for discovery information
- Useful for new unknown fields

In produzione è bene definire uno schema per verificare i dati che vengono indicizzati

-------------------------

**Mapping**

- Custom mappings are the base for:
  - Elasticsearch try to create the best mapping
  - Optimizing Elasticsearch both space and time
- Advanced modelling Custom
  - Analizers Multifielad
  - relations
    - nested



**Change Mapping**

- Mapping are additive:
  - non è possibile modificare i campi a runtime
  - non possibile eliminare il mapping
- For changing mappings the steps are the above:
  - Create a new index with the new mappings
  - reaindex all the records
  - delete the old index

1. è costoso ma è l'unico modo
2. devono essere usati gli **<u>alias</u>**! Lato applicativo bisogna sempre far riferimento  all'alias!



NB: è possibile fare dei reindex utilizzando delle query per applicarlo solo ad un subset di dati

-----------------

**Mapping Properies**

- index (default "true") configura i campi che devono essere indicizzati
  - i valori ammessi sono:
    - false: il campo non viene indicizzato, utile per i dati che non devono essere ricercabili
    - true: il campo viene analizzato attraverso l'analyzer configurato

NB: quando posso non indicizzo, meno dati ho indicizzato, più piccolo sarà l'inverted index di elasti e più saranno veloci le query di search!

- index_analyzer (defaul: null) definisce quale analyzer viene usato per processare il dato
  - search_analyzer (defaul: null)  definisce quale analyzer viene utilizzato in fase di ricerca
  - analyzer imposta l'analyzer sia per la ricerca che per i dati 

**Dynamic Field Mapping**

di default i campi posso essere aggiunti dinamicamente ad un documento, questi vengono aggiunti al mapping

dynamic: consente evitare l'aggiunta dinamica di campi

 - true: nuovi dati trovati vengono aggiunti al mapping
 - false: i nuovi campi vengono ignorati e non aggiunti al mapping, il documento viene indicizzato, il campo non viene indicizzato e quindi non è ricercabile
 - string: se un nuovo campo viene trovato all'interno del documento viene sollevata un eccezione e il documento non viene indicizzato 

**Copy_to Field Mapping**

- peremtte di create un custom field nel quale vengono copiati i valori dei campi indicati
- il campo custom consente di effettuare delle query su un singolo campo

NB: viene utlizzato per ottimizzare le query, anzichè fare query su 10 campi, è possibile farla su un signolo campo

**Coerce Field Mapping**

abilita il casting automatico dei dati

**Enable Field Mapping**

- consente di disabilitare la ricerca su determinati campi
- può essere applicato solomamente su mapping type o object type

**Document Meta Flieds**

Gli attributi più importanti per i meta dati di un documento sono:

- _id
- _type
- _index
- _size
- _version
- _source: contenuto informativo
- _routing: controlla in quale shard store i documenti saranno inseriti

_________________________________

**Dynamic Templates**

- consente di creare dei template che pilota il dynamic mapping

_____________________

**Nested Data Type**

- Sono oggetti che vengono indicizzati normalemente ma elastic tratta in maniera differente nel processing e nella search
- Consente di poter ricercare oggetti all'interno di un array in maniera indipendente

___________________

**JOIN Datatype**

- un campo speciale che consente di creare relazioni padre/figlio all'interno di un documento di uno stesso indice
- per indicizzare un documento con una join la relazione deve essere indicata all'interno del source del documento
- l'indicizzazione si differenzia tra parent e children, il children deve indicare il routing ed il parent
- le join non devono essere considerate come le relazioni dei db relazionali

---------------

**Range Datatypes**

- posso indicizzare definiendo un valore minimo e un vaolre massimo

---------------

**Fields Mapping**

- spesso è molto utile indicizzare un informazione più volte in modalità diverse

------------



Come Elastiche indicizza e cosa lucene fa per elastic



Su un testo: 

- viene eseguito una tokenizer
- crea una lista di token normalizati (ad esempio mette tutto in lower case)
- viene costruito l'inverted index, ovvero una mappa sui token

_________________

**Anatomy of an Analyzer**

- character filters
- tokenizers
- Token Filters

Questi possono essere combinati per cofigurare custom analy<ers per index

------

**Built-in Analyzers**

 - standard - default
 - simple - spezza il testo in termini ovunque incontra un carattere che non è una lettera
 - keyword - indicizza il testo esattamente com'è
 - Others:
    - whitespace, stop, pattern, language

--------------

**Index Templates**

consentono di definire dei template che vengono applicati alla creazione degli indici, creando un mapping specifico. Il template viene applicato in base ad un pattern sul nome dell'indice.

Ovviamente è possibile creare, cancellare e visualizzare i templati attravero rest api.

- Multiple Templates Matching
  - più di un template più matchare un indce
  - è possibile gestire la casisitica attraverso l'attributo *order*

-------------

**Index a Documet**

--vedere esempi da slide

- attraverso l'operazione create ci si può assicurare di non sovrascivere un documento
- refresh alla callback si ha la certezza che il documento è stato indicizzato 
  - ha impatto sulla risposta

--------------------------------------



## Search

![1548846868267](/home/davide/.config/Typora/typora-user-images/1548846868267.png)



**Sezioni:**

 - search
 - filter (i filtri sono calcolati in base ai risultati della ricerca - devono essere recuperati tramire una richiesta diversa da quella dei risultati, in quanto difficilmente cambieranno in un tempo breve, questo permette di ottimizzare le richeiste)
 - result 
 - pagination



**Search execution:**

1. Client app contatta il coordinatign node
2. La query viene effettauto in broadcast ad una shard copy di ogni shard dell'indice
   1. ogni shard esegue localmente la query che viene detta *MAP*
3. Ogni shard restituisce gli ID dei document ordinati per i top hits al coordinating node
4. Il coordinating node fa un merge dei valori degli ID e crea una lista ordinata di tutti i risultati
5. A questo punto il coordinating node conosce il top 10 hits e può recuperare i documenti
6. Il coordinating node restituisce i doumenti all'app client

---------------

**Relevance**

- La rilevanza è un informazione (un valore numerico) che rappresenta quanto il documento è rilevante riguardo una specifica query
- Nel json risultante da una query, l'attributo *_score* indica il valore della rilevanza
- Elastic usa l'algoritmom BM25 per calcolarla
- Viene calcola in base a 3 fattori:
  - Frequenza dei termini (parole)
  - Frequenza Inverse Document
  - Dimensione dei campi



![1548847921626](/home/davide/.config/Typora/typora-user-images/1548847921626.png)

![1548847940151](/home/davide/.config/Typora/typora-user-images/1548847940151.png)

--------------------

**Boolean Query**

- tutte le query all'interno di una clausola *must* di default sono in *and*
- tutte le query all'interno di una clausola *should* di default sono in *or*
- La clausola *should* usata in combinazione con la clausola *must* assume un comportamente differente, ovvero incide sulla rilevanza e non sulla selezione dei documenti

- le query range non incidono sulla rilevanza, quindi per ottimizzare si può inserire le query  di range nella clausola di filter

------------

**Nested Query**

- se uso una query normale su un oggetto nested non ottengo risultati

------------

**Join Query**

- le query di tipo join possono essere utilizzate solo se ho definito il tipo di relazione nel mappig del document

--------------------

**Aggregations**

Tipologie di aggregazione:

- Bucket
- Metric
- Pipeline

Le aggregazioni possono essere innestate



----------------------------------

Spunti interessanti:

- https://elastic.github.io/eui/#/charts-deprecated/general
- https://vega.github.io/vega/