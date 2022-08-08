# Strutture Dati Base

## Usare un array per memorizzare una collezione di dati
Di seguito è riportato un esempio della più semplice implementazione di una struttura dati ad array. Questo è conosciuto come array uni-dimensionale, il che significa che ha un solo livello, o che non ha altri array annidati al suo interno. Nota che contiene booleani, stringhe e numeri, tra gli altri tipi di dati JavaScript validi:
```js
let simpleArray = ['one', 2, 'three', true, false, undefined, null];
console.log(simpleArray.length);
```
La chiamata console.log stampa 7.

Tutti gli array hanno una proprietà di lunghezza, che come mostrato sopra, può essere facilmente accessibile con la sintassi Array.length. Un'implementazione più complessa di un array può essere vista qui sotto. Questo è conosciuto come array multi-dimensionale, e si tratta di un array che contiene altri array. Nota che questo array contiene anche oggetti JavaScript, che esamineremo molto attentamente nella nostra prossima sezione, ma per ora, tutto quello che devi sapere è che gli array sono anche in grado di memorizzare oggetti complessi.
```js
let complexArray = [
  [
    {
      one: 1,
      two: 2
    },
    {
      three: 3,
      four: 4
    }
  ],
  [
    {
      a: "a",
      b: "b"
    },
    {
      c: "c",
      d: "d"
    }
  ]
];
```

--- 
## Accedere ai contenuti dell'array usando la notazione a parentesi
La caratteristica fondamentale di qualsiasi struttura di dati è, ovviamente, la capacità non solo di memorizzare i dati, ma di essere in grado di recuperare tali dati a comando. Quindi, adesso che abbiamo imparato a creare un array, cominciamo a pensare come possiamo accedere alle informazioni di quell'array.

Se definiamo un semplice array come il seguente, ci sono 3 elementi:
```js
let ourArray = ["a", "b", "c"];
```
In un array, ogni elemento ha un indice. Questo indice indica la posizione di quell'elemento nell'array e come lo puoi consultare. Tuttavia è importante notare che gli array JavaScript sono indicizzati a zero, cioè che il primo elemento di un array è in realtà alla zeresima posizione, non alla prima. Per recuperare un elemento da un array possiamo racchiudere un indice tra parentesi e aggiungerlo alla fine di un array, o più comunemente, a una variabile che fa riferimento ad un array. Questa notazione si chiama notazione a parentesi. Ad esempio, se vogliamo recuperare a da ourArray e assegnarlo a una variabile, possiamo farlo con il seguente codice:
```js
let ourVariable = ourArray[0];
```
Ora ourVariable ha il valore di a.

Oltre ad accedere al valore associato ad un indice, è anche possibile impostare un indice ad un valore utilizzando la stessa notazione:
```js
ourArray[1] = "not b anymore";
```
Usando la notazione tra parentesi, abbiamo resettato l'elemento all'indice 1 dalla stringa b, alla stringa not b anymore. Ora ourArray è ["a", "not b anymore", "c"].

---

## Aggiungere elementi ad un array con push() e unshift()
La lunghezza di un array, così come i tipi di dati che può contenere, non è fissata. Gli array possono essere definiti con un numero qualsiasi di elementi, e gli elementi possono essere aggiunti o rimossi nel tempo; in altre parole, gli array sono mutabili. In questa sfida, esamineremo due metodi con cui possiamo modificare programmaticamente un array: Array.push() e Array.unshift().

Entrambi i metodi prendono uno o più elementi come parametri e aggiungono questi elementi all'array su cui il metodo è stato chiamato; il metodo push() aggiunge elementi alla fine di un array, e unshift() aggiunge elementi all'inizio. Considera quanto segue:
```js
let twentyThree = 'XXIII';
let romanNumerals = ['XXI', 'XXII'];

romanNumerals.unshift('XIX', 'XX');
```
romanNumerals avrà i valori ['XIX', 'XX', 'XXI', 'XXII'].
```js
romanNumerals.push(twentyThree);
```
romanNumerals avrà i valori ['XIX', 'XX', 'XXI', 'XXII', 'XXIII']. Nota che possiamo anche passare variabili, il che ci permette una flessibilità ancora maggiore nel modificare dinamicamente i dati del nostro array.

---

## Rimuovere elementi da un array con pop() e shift()
Sia push() che unshift() hanno metodi corrispondenti che sono quasi funzionalmente opposti: pop() e shift(). Come forse avrai già indovinato, invece di aggiungere, pop() rimuove un elemento dalla fine di un array, mentre shift() rimuove un elemento dall'inizio. La differenza chiave tra pop() e shift() e i loro cugini push() e unshift(), è che nessuno dei due metodi richiede parametri, e ognuno permette che l'array venga modificato di un solo elemento per volta.

Diamo un'occhiata:
```js
let greetings = ['whats up?', 'hello', 'see ya!'];

greetings.pop();
```
greetings avrà il valore ['whats up?', 'hello'].
```js
greetings.shift();
```
greetings avrà il valore ['hello'].

Con entrambi i metodi possiamo anche restituire il valore dell'elemento rimosso in questo modo:
```js
let popped = greetings.pop();
```
greetings avrà il valore [] e popped avrà il valore hello.

---

## Rimuovere elementi usando splice()
Ok, quindi abbiamo imparato a rimuovere gli elementi dall'inizio e dalla fine degli array usando shift() e pop(), ma cosa succede se vogliamo rimuovere un elemento da qualche parte nel mezzo? O rimuovere più di un elemento alla volta? Beh, ecco dove entra in gioco splice(). splice() ci permette di fare proprio questo: rimuovere qualunque numero di elementi consecutivi da qualsiasi punto di un array.

splice() può richiedere fino a 3 parametri, ma per ora ci concentreremo solo sui primi 2. I primi due parametri di splice() sono interi che rappresentano indici, o posizioni, dell'array sul quale viene chiamato splice(). E ricorda, gli array sono indicizzati a zero, quindi per indicare il primo elemento di un array, useremo 0. Il primo parametro di splice()rappresenta l'indice dell'array da cui iniziare a rimuovere gli elementi, mentre il secondo parametro indica il numero di elementi da eliminare. Ad esempio:
```js
let array = ['today', 'was', 'not', 'so', 'great'];

array.splice(2, 2);
```
Qui rimuoviamo 2 elementi a partire dal terzo (all'indice 2). array avrà il valore ['today', 'was', 'great'].

splice() non solo modifica l'array su cui viene chiamato, ma restituisce anche un nuovo array contenente il valore degli elementi rimossi:
```js
let array = ['I', 'am', 'feeling', 'really', 'happy'];

let newArray = array.splice(3, 2);
```
newArray ha il valore ['really', 'happy'].

----

## Aggiungere elementi usando splice()
Ricordi che nell'ultima sfida abbiamo detto che splice() può richiedere fino a tre parametri? Bene, è possibile utilizzare il terzo parametro, composto da uno o più elementi, per aggiungerli all'array. Questo può essere incredibilmente utile per scambiare rapidamente un elemento, o un insieme di elementi, con un altro.
```js
const numbers = [10, 11, 12, 12, 15];
const startIndex = 3;
const amountToDelete = 1;

numbers.splice(startIndex, amountToDelete, 13, 14);
console.log(numbers);
```
La seconda occorrenza di 12 viene rimossa, e aggiungiamo 13 e 14 allo stesso indice. L'array numbers ora è [ 10, 11, 12, 13, 14, 15 ].

Qui iniziamo con una serie di numeri. Poi, passiamo i seguenti dati a splice(): L'indice a cui iniziare a eliminare gli elementi (3), il numero di elementi da eliminare (1) e i restanti argomenti (13, 14) saranno inseriti a partire dallo stesso indice. Nota che ci può essere un numero qualsiasi di elementi (separati da virgole) dopo amountToDelete, ognuno dei quali verrà inserito.

--- 

## Copiare elementi degli array usando slice()
Il prossimo metodo che tratteremo è slice(). Invece di modificare un array, slice() copia o estrae un dato numero di elementi in un nuovo array, lasciando intatto l'array su cui è chiamato. slice() richiede solo 2 parametri — il primo è l'indice a cui iniziare l'estrazione, e il secondo è l'indice al quale interrompere l'estrazione (l'estrazione avverrà fino all'elemento a questo indice, che però non sarà incluso). Considera:
```js
let weatherConditions = ['rain', 'snow', 'sleet', 'hail', 'clear'];

let todaysWeather = weatherConditions.slice(1, 3);
```
todaysWeather avrà il valore ['snow', 'sleet'], mentre weatherConditions sarà ancora ['rain', 'snow', 'sleet', 'hail', 'clear'].

Di fatto, abbiamo creato un nuovo array estraendo elementi da un array esistente.

---

## Copiare un array con l'operatore di propagazione
Mentre slice() ci permette di essere selettivi su quali elementi di un array copiare, tra diverse altre attività utili, il nuovo operatore di propagazione di ES6 ci permette di copiare facilmente tutti gli elementi di un array, in ordine, con una sintassi semplice e molto leggibile. La sintassi di propagazione è semplicemente questa: ...

In pratica, possiamo usare l'operatore di propagazione per copiare un array in questo modo:
```js
let thisArray = [true, true, undefined, false, null];
let thatArray = [...thisArray];
```
thatArray è uguale a [true, true, undefined, false, null]. thisArray rimane invariato e thatArray contiene gli stessi elementi di thisArray.

--- 

## Combinare gli array con l'operatore di propagazione
Un altro enorme vantaggio dell'operatore di propagazione è la capacità di combinare array, o di inserire tutti gli elementi di un array in un altro, a partire da qualsiasi indice. Con le sintassi più tradizionali, possiamo concatenare array, ma questo ci permette solo di unire array alla fine di uno, e all'inizio di un altro. La sintassi di propagazione rende estremamente semplice la seguente operazione:
```js
let thisArray = ['sage', 'rosemary', 'parsley', 'thyme'];

let thatArray = ['basil', 'cilantro', ...thisArray, 'coriander'];
```
thatArray avrà i valori ['basil', 'cilantro', 'sage', 'rosemary', 'parsley', 'thyme', 'coriander'].

Utilizzando la sintassi di propagazione, abbiamo appena realizzato un'operazione che sarebbe stata più complessa e più prolissa se avessimo usato metodi tradizionali.

--- 

## Verificare la presenza di un elemento con indexOf()
Dal momento che gli array possono essere cambiati, o mutati, in qualsiasi momento, non c'è alcuna garanzia su dove sia un particolare dato in un determinato array, o se quell'elemento esista ancora. Fortunatamente, JavaScript ci fornisce un altro metodo nativo, indexOf(), che ci permette di controllare rapidamente e facilmente la presenza di un elemento in un array. indexOf() prende un elemento come parametro, e quando chiamato, restituisce la posizione, o indice, di quell'elemento, o -1 se l'elemento non è presente nell'array.

Ad esempio:
```js
let fruits = ['apples', 'pears', 'oranges', 'peaches', 'pears'];

fruits.indexOf('dates');
fruits.indexOf('oranges');
fruits.indexOf('pears');
```
indexOf('dates') restituisce -1, indexOf('oranges') restituisce 2e indexOf('pears') restituisce 1 (il primo indice in cui è presente il rispettivo elemento).

--- 
## Iterare attraverso tutti gli oggetti di un array utilizzando i cicli for
A volte, quando si lavora con gli array, è molto utile essere in grado di iterare attraverso ogni elemento per trovare uno o più elementi di cui potremmo aver bisogno, o per manipolare un array basandoci sugli elementi che soddisfano una determinata serie di criteri. JavaScript offre diversi metodi integrati, ognuno dei quali itera sugli array in modo leggermente differente dagli altri per ottenere risultati diversi (come every(), forEach(), map(), etc.), tuttavia la tecnica più flessibile e che ci offre la massima quantità di controllo è un semplice ciclo for.

Considera quanto segue:
```js
function greaterThanTen(arr) {
  let newArr = [];
  for (let i = 0; i < arr.length; i++) {
    if (arr[i] > 10) {
      newArr.push(arr[i]);
    }
  }
  return newArr;
}

greaterThanTen([2, 12, 8, 14, 80, 0, 1]);
```
Utilizzando un ciclo for, questa funzione itera attraverso ogni elemento dell'array, vi accede e lo sottopone a un semplice test che abbiamo creato. In questo modo, abbiamo determinato facilmente e in maniera schematica quali dati sono maggiori di 10, e abbiamo restituito un nuovo array, [12, 14, 80], contenente questi elementi.

---

## Creare array multi-dimensionali complessi

Una delle caratteristiche più potenti quando si pensa agli array come strutture di dati, è che gli array possono contenere, o anche essere completamente costituiti da altri array. Abbiamo visto array che contengono altri array nelle sfide precedenti, ma erano abbastanza semplici. Tuttavia, gli array possono contenere una profondità infinita di array che possono contenere altri array, ciascuno con i propri livelli arbitrari di profondità, e così via. In questo modo, un array può diventare in fretta una struttura dati molto complessa, nota come multi-dimensionale, o array annidato. Considera l'esempio seguente:
```js
let nestedArray = [
  ['deep'],
  [
    ['deeper'], ['deeper'] 
  ],
  [
    [
      ['deepest'], ['deepest']
    ],
    [
      [
        ['deepest-est?']
      ]
    ]
  ]
];
```
L'array deep è annidato al secondo livello di profondità. Gli array deeper sono al terzo livello di profondità. Gli array deepest al quarto livello, e il deepest-est? è al quinto.

Anche se questo esempio può sembrare contorto, questo livello di complessità non è inaudito, e nemmeno insolito, quando si tratta di grandi quantità di dati. Tuttavia, possiamo ancora accedere molto facilmente ai livelli più profondi di un array così complesso con la notazione tra parentesi:
```js
console.log(nestedArray[2][1][0][0][0]);
```
Questo mostra nella console la stringa deepest-est?. E ora che sappiamo dove sono i dati, possiamo reimpostarli se ne abbiamo bisogno:
```js
nestedArray[2][1][0][0][0] = 'deeper still';

console.log(nestedArray[2][1][0][0][0]);
```
Ora verrà scritto deeper still.

--- 

## Aggiungere coppie chiave-valore agli oggetti JavaScript
In linea di massima, gli oggetti sono solo collezioni di coppie chiave-valore. In altre parole, sono dati (valori) mappati da identificatori univoci chiamati proprietà (chiavi). Dai un'occhiata ad un esempio:
```js
const tekkenCharacter = {
  player: 'Hwoarang',
  fightingStyle: 'Tae Kwon Doe',
  human: true
};
```
Il codice qui sopra definisce l'oggetto di un personaggio del videogioco Tekken, chiamato tekkenCharacter. Ha tre proprietà, ad ognuna delle quali corrisponde un valore specifico. Se desiderassi aggiungere una nuova proprietà, ad esempio "origin", potresti farlo assegnando origin all'oggetto:
```js
tekkenCharacter.origin = 'South Korea';
```
Questo usa la notazione a punti. Se tu osservi l'oggetto tekkenCharacter, esso ora includerà la proprietà origin. Hwoarang aveva anche dei caratteristici capelli arancioni. È possibile aggiungere questa proprietà con la notazione a parentesi scrivendo:
```js
tekkenCharacter['hair color'] = 'dyed orange';
```
La notazione a parentesi è obbligatoria se la proprietà ha uno spazio o se si vuole utilizzare una variabile per selezionare la proprietà. Nel caso precedente, la proprietà è racchiusa tra virgolette per indicarla come una stringa e verrà aggiunta esattamente come mostrato. Senza virgolette, sarà valutata come una variabile e il nome della proprietà sarà qualsiasi valore sia assegnato alla variabile. Ecco un esempio con una variabile:
```js
const eyes = 'eye color';

tekkenCharacter[eyes] = 'brown';
```
Dopo aver aggiunto tutti gli esempi, l'oggetto apparirà così:
```js
{
  player: 'Hwoarang',
  fightingStyle: 'Tae Kwon Doe',
  human: true,
  origin: 'South Korea',
  'hair color': 'dyed orange',
  'eye color': 'brown'
};
```

---

## Modificare un oggetto annidato in un altro oggetto
Diamo adesso un'occhiata ad un oggetto leggermente più complesso. Le proprietà dell'oggetto possono essere annidate ad una profondità arbitraria, e i loro valori possono essere qualsiasi tipo di dati supportato da JavaScript, inclusi array ed altri oggetti. Considera quanto segue:
```js
let nestedObject = {
  id: 28802695164,
  date: 'December 31, 2016',
  data: {
    totalUsers: 99,
    online: 80,
    onlineStatus: {
      active: 67,
      away: 13,
      busy: 8
    }
  }
};
```
nestedObject ha tre proprietà: id (il valore è un numero), date (il valore è una stringa) e data (il valore è un oggetto con la propria struttura annidata). Anche se le strutture possono diventare rapidamente complesse, è ancora possibile utilizzare le stesse notazioni per accedere alle informazioni di cui abbiamo bisogno. Per assegnare il valore 10 alla proprietà busy dell'oggetto annidato onlineStatus, usiamo la notazione a punti per fare riferimento alla proprietà:
```js
nestedObject.data.onlineStatus.busy = 10;
```

--- 

## Accedere ai nomi delle proprietà con la notazione a parentesi
Nella prima sfida sugli oggetti abbiamo menzionato l'uso della notazione a parentesi come modo per accedere ai valori delle proprietà utilizzando la valutazione di una variabile. Per esempio, immagina che il nostro oggetto foods venga utilizzato in un programma per il registratore di cassa di un supermercato. Abbiamo una funzione che imposta selectedFood e vogliamo controllare se nel nostro oggetto foods è presente quel cibo. Questo potrebbe apparire così:
```js
let selectedFood = getCurrentFood(scannedItem);
let inventory = foods[selectedFood];
```
Questo codice valuterà il valore memorizzato nella variabile selectedFood e restituirà il valore di quella proprietà nell'oggetto foods, oppure undefined se non è presente. La notazione a parentesi è molto utile perché a volte le proprietà dell'oggetto non sono note prima dell'esecuzione o abbiamo bisogno di accedervi in modo più dinamico.

---

## Utilizzare la parola chiave delete per rimuovere proprietà da un oggetto
Ora sai cosa sono gli oggetti e quali sono le loro caratteristiche e vantaggi di base. In breve, si tratta di archivi di coppie chiave-valore che dispongono di un modo flessibile e intuitivo di strutturare i dati, e, assicurano un tempo di ricerca molto veloce. Nel resto di queste sfide, descriveremo diverse operazioni comuni che puoi eseguire sugli oggetti in modo che tu possa acquisire dimestichezza nell'applicare queste utili strutture di dati nei tuoi programmi.

Nelle sfide precedenti, abbiamo sia aggiunto che modificato le coppie chiave-valore di un oggetto. Qui vedremo come possiamo rimuovere una coppia chiave-valore da un oggetto.

Rivisitiamo il nostro esempio di oggetto foods un'ultima volta. Se volessimo rimuovere la chiave apples, possiamo eliminarla utilizzando la parola chiave delete in questo modo:
```js
delete foods.apples;
```

---

## Verificare se un oggetto ha una proprietà
Adesso possiamo aggiungere, modificare e rimuovere chiavi dagli oggetti. Ma se volessimo solo sapere se un oggetto ha una determinata proprietà? JavaScript ci fornisce due modi diversi per farlo. Uno utilizza il metodo hasOwnProperty() e l'altro usa la parola chiave in. Se abbiamo un oggetto users con una proprietà Alan, potremmo verificare la sua presenza in uno dei seguenti modi:
```js
users.hasOwnProperty('Alan');
'Alan' in users;
```
Entrambi restituirebbero true.

---

## Iterare attraverso le chiavi di un oggetto con l'istruzione for...in
A volte potrebbe essere necessario iterare attraverso tutte le chiavi di un oggetto. Ciò richiede una sintassi specifica in JavaScript chiamata istruzione for...in. Per il nostro oggetto users, questo potrebbe assomigliare a:
```js
for (let user in users) {
  console.log(user);
}
```
Che scriverebbe Alan, Jeff e Sarah sulla console - ogni valore sulla propria riga.

In questa dichiarazione abbiamo definito una variabile user, e come puoi vedere, mentre l'iterazione prosegue attraverso l'oggetto, ad ogni ripetizione la variabile viene reimpostata a ciascuna delle chiavi, risultando nella stampa del nome di ogni utente sulla console.

NOTA: Gli oggetti non mantengono un ordine sulle chiavi memorizzate come fanno gli arrays; di conseguenza la posizione di una chiave in un oggetto, o l'ordine relativo in cui appare, è irrilevante quando ci si riferisce a tale chiave o vi si accede.

---

## Creare l'array delle proprietà con Object.keys()
Possiamo anche generare un array che contiene tutte le chiavi memorizzate in un oggetto con il metodo **Object.keys()**. Questo metodo prende un oggetto come argomento e restituisce un array di stringhe che rappresentano ciascuna proprietà nell'oggetto. Di nuovo, non ci sarà alcun ordine specifico per gli elementi nell'array.
```js
let users = {
  Alan: {
    age: 27,
    online: false
  },
  Jeff: {
    age: 32,
    online: true
  },
  Sarah: {
    age: 48,
    online: false
  },
  Ryan: {
    age: 19,
    online: true
  }
};

function getArrayOfUsers(obj) {
  return Object.keys(obj); 
}

console.log(getArrayOfUsers(users));
```

---

## Modificare un array memorizzato in un oggetto
Adesso hai visto tutte le operazioni di base per gli oggetti JavaScript. Puoi aggiungere, modificare e rimuovere coppie chiave-valore, controllare se una proprietà esiste e iterare su tutte le chiavi di un oggetto. Continuando a conoscere JavaScript vedrai applicazioni ancora più versatili degli oggetti. Inoltre, le lezioni di Strutture Dati nella sezione Colloquio di Lavoro per Programmatori del curriculum coprono anche gli oggetti ES6 Map e Set, entrambi i quali sono simili a oggetti ordinari, ma forniscono alcune caratteristiche aggiuntive. Ora che hai imparato le basi di array e oggetti, sei pienamente preparato per iniziare ad affrontare problemi più complessi utilizzando JavaScript!

Es: L'oggetto user contiene tre chiavi. La chiave data contiene cinque chiavi, una delle quali contiene un array di friends (amici). Da questo puoi vedere quanto gli oggetti siano flessibili come strutture di dati. Abbiamo iniziato a scrivere una funzione addFriend. Finisci di scriverla in modo che prenda un oggetto user, aggiunga il nome dell'argomento friend all'array memorizzato in user.data.friends e restituisca questo array.

```js
let user = {
  name: "Kenneth",
  age: 28,
  data: {
    username: "kennethCodesAllDay",
    joinDate: "March 26, 2016",
    organization: "freeCodeCamp",
    friends: ["Sam", "Kira", "Tomo"],
    location: {
      city: "San Francisco",
      state: "CA",
      country: "USA"
    }
  }
};

function addFriend(userObj, friend) {
  userObj.data.friends.push(friend);
  return userObj.data.friends;
}

console.log(addFriend(user, "Pete"));
```