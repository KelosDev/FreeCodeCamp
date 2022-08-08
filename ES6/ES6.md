# ES6

## Prevenire la mutazione degli oggetti

La dichiarazione **const** da sola non protegge davvero i tuoi dati dalla mutazione. Per garantire che i tuoi dati non cambino, JavaScript fornisce una funzione Object.freeze per prevenire la mutazione dei dati.

Qualsiasi tentativo di cambiare l'oggetto verrà rifiutato, con un errore generato se lo script viene eseguito in modalità rigorosa.
```js
    let obj = {
    name:"FreeCodeCamp",
    review:"Awesome"
    };
    Object.freeze(obj);
    obj.review = "bad";
    obj.newProp = "Test";
    console.log(obj);
```
Gli assegnamenti obj.review e obj.newProp provocheranno errori, perché il nostro editor viene eseguito in modalità rigorosa per impostazione predefinita, e la console visualizzerà il valore { name: "FreeCodeCamp", review: "Awesome" }.

---

## Impostare parametri predefiniti per le tue funzioni

Per aiutarci a creare funzioni più flessibili, ES6 introduce dei parametri predefiniti per le funzioni.

Dai un'occhiata a questo codice:

```js
const greeting = (name = "Anonymous") => "Hello " + name;

console.log(greeting("John"));
console.log(greeting());
```
La console mostrerà le stringhe Hello John e Hello Anonymous.

Il parametro predefinito entra in gioco quando l'argomento non è specificato (è indefinito). Come puoi vedere nell'esempio qui sopra, il parametro name riceverà il suo valore predefinito Anonymous quando non si fornisce un valore per il parametro. Puoi aggiungere valori predefiniti per tutti i parametri che vuoi.

---

## Usare il parametro resto con gli argomenti delle funzioni

Per aiutarci a creare funzioni più flessibili, ES6 introduce il parametro resto per i parametri di funzioni. Con il parametro resto, è possibile creare funzioni che richiedono un numero variabile di argomenti. Questi argomenti sono memorizzati in un array a cui è possibile accedere successivamente dall'interno della funzione.

Dai un'occhiata a questo codice:
```js
function howMany(...args) {
  return "You have passed " + args.length + " arguments.";
}
console.log(howMany(0, 1, 2));
console.log(howMany("string", null, [1, 2, 3], { }));
```
La console mostrerà le stringhe You have passed 3 arguments. e You have passed 4 arguments..

Il parametro resto elimina la necessità di controllare l'array args e ci permette di applicare map(), filter() e reduce() all'array dei parametri.

---

## Usare l'operatore di propagazione per analizzare gli array in-place

ES6 introduce l'operatore di propagazione, che ci permette di espandere array ed altre espressioni in posizioni dove sono attesi più parametri o elementi.

Il codice ES5 qui sotto utilizza apply() per calcolare il valore massimo in un array:
```js
var arr = [6, 89, 3, 45];
var maximus = Math.max.apply(null, arr);
```
maximus avrà un valore di 89.
Abbiamo dovuto utilizzare Math.max.apply(null, arr) perché Math.max(arr) restituisce NaN. Math.max() si aspetta argomenti separati da virgole, ma non un array. L'operatore di propagazione rende questa sintassi molto migliore da leggere e mantenere.

const arr = [6, 89, 3, 45];
const maximus = Math.max(...arr);
maximus avrà un valore di 89.

...arr restituisce un array spacchettato. In altre parole, propaga l'array. Tuttavia, l'operatore di propagazione funziona solo sul posto, come argomento di una funzione o in un array letterale (definito usando le parentesi quadre). Il seguente codice non funzionerà:
```js
const spreaded = ...arr;
```

---

## Usare l'assegnazione destrutturante per estrarre valori dagli oggetti

L'assegnazione destrutturante è una sintassi speciale introdotta in ES6, per assegnare efficacemente dei valori presi da un oggetto.

Considerare il seguente codice ES5:
```js
const user = { name: 'John Doe', age: 34 };

const name = user.name;
const age = user.age;
```
name avrebbe come valore la stringa John Doe, e age avrebbe il numero 34.

Ecco una dichiarazione di assegnazione equivalente che utilizza la sintassi di destrutturazione ES6:
```js
const { name, age } = user;
```
Ancora una volta, name avrà come valore la stringa John Doe, e age il numero 34.

Qui, le variabili name e age verranno create e assegnate ai rispettivi valori nell'oggetto user. Puoi constatare quanto questo sia più pulito.

Potrai estrarre dall'oggetto tutti i valori che desideri.

---

## Usare l'assegnazione destrutturante per assegnare variabili dagli oggetti

La destrutturazione ti consente di assegnare un nuovo nome di variabile mentre si estraggono i valori. Puoi farlo inserendo il nuovo nome dopo i due punti quando assegni il valore.

Usando lo stesso oggetto dell'ultimo esempio:
```js
const user = { name: 'John Doe', age: 34 };
```
Ecco come è possibile creare nuovi nomi di variabili con l'assegnazione:
```js
const { name: userName, age: userAge } = user;
```
Lo puoi leggere come "prendi il valore di user.name e assegnalo ad una nuova variabile chiamata userName" e così via. Il valore di userName sarà la stringa John Doe, e il valore di userAge sarà il numero 34.

---

## Usare l'assegnazione destrutturante per assegnare variabili da oggetti annidati

È possibile utilizzare gli stessi principi delle due lezioni precedenti per destrutturare valori da oggetti annidati.

Usando un oggetto simile agli esempi precedenti:
```js
const user = {
  johnDoe: { 
    age: 34,
    email: 'johnDoe@freeCodeCamp.com'
  }
};
```
Ecco come estrarre i valori delle proprietà dell'oggetto e assegnarli a variabili con lo stesso nome:
```js
const { johnDoe: { age, email }} = user;
```
Ed ecco come puoi assegnare i valori delle proprietà di un oggetto a variabili con nomi diversi:
```js
const { johnDoe: { age: userAge, email: userEmail }} = user;
```

---

## Usare l'assegnazione destrutturante per assegnare variabili dagli array

ES6 rende la destrutturazione degli array facile come quella degli oggetti.

Una differenza fondamentale tra l'operatore di propagazione e la destrutturazione dell'array è che l'operatore di diffusione spacchetta tutti i contenuti di un'array in una lista separata da virgole. Di conseguenza, non è possibile selezionare o scegliere quali elementi si desidera assegnare a delle variabili.

La destrutturazione di un array ci permette di fare esattamente questo:
```js
const [a, b] = [1, 2, 3, 4, 5, 6];
console.log(a, b);
```
La console mostrerà i valori di a e b come 1, 2.

Alla variabile a viene assegnato il primo valore dell'array, e a b viene assegnato il secondo valore dell'array. Possiamo anche accedere al valore a qualsiasi indice di un array tramite destrutturazione, utilizzando le virgole per raggiungere l'indice desiderato:
```js
const [a, b,,, c] = [1, 2, 3, 4, 5, 6];
console.log(a, b, c);
```
La console mostrerà i valori di a, b, e c come 1, 2, 5.

---

## Usare l'assegnazione destrutturante con il parametro di resto per riassegnare gli elementi dell'array

In alcune situazioni che comportano la destrutturazione di array, potremmo voler raccogliere il resto degli elementi in un array separato.

Il risultato è simile a Array.prototype.slice(), come mostrato sotto:
```js
const [a, b, ...arr] = [1, 2, 3, 4, 5, 7];
console.log(a, b);
console.log(arr);
```
La console mostrerà i valori 1, 2 e [3, 4, 5, 7].

Le variabili a e b prendono il primo e il secondo valore dall'array. Dopodiché, a causa della presenza del parametro di resto, arr ottiene il resto dei valori sotto forma di un array. L'elemento di resto funziona correttamente solo come ultima variabile dell'elenco. Non è quindi possibile utilizzare il parametro di resto per catturare un sottoarray che lascia fuori l'ultimo elemento dell'array originale.

---

## Usare l'assegnazione destrutturante per passare un oggetto come parametro a una funzione

In alcuni casi, è possibile destrutturare l'oggetto in un argomento funzione.

Considera il codice qui sotto:
```js
const profileUpdate = (profileData) => {
  const { name, age, nationality, location } = profileData;
}
```
Questo destruttura efficacemente l'oggetto passato alla funzione. Questo può anche essere fatto sul posto:
```js
const profileUpdate = ({ name, age, nationality, location }) => {}
```
Quando profileData viene passato alla funzione qui sopra, i valori del parametro vengono destrutturati per l'utilizzo all'interno della funzione.

---

## Scorciatoier sulle proprietà

ES6 aggiunge un bel supporto per definire facilmente gli oggetti letterali.

Considera il seguente codice:
```js
const getMousePosition = (x, y) => ({
  x: x,
  y: y
});
```
getMousePosition è una semplice funzione che restituisce un oggetto contenente due proprietà. ES6 fornisce lo zucchero sintattico per eliminare la ridondanza di dover scrivere x: x. Puoi semplicemente scrivere x una volta, e verrà convertito in x: x (o qualcosa di equivalente) dietro le quinte. Ecco la stessa funzione di cui sopra, riscritta utilizzando questa nuova sintassi:
```js
const getMousePosition = (x, y) => ({ x, y });
```

---

## Scrivere funzioni dichiarative concise con ES6

Quando si definiscono le funzioni all'interno degli oggetti in ES5, dobbiamo usare la parola chiave function come segue:
```js
const person = {
  name: "Taylor",
  sayHello: function() {
    return `Hello! My name is ${this.name}.`;
  }
};
```
Con ES6, è possibile rimuovere simultaneamente la parola chiave function e i due punti quando si definiscono le funzioni negli oggetti. Ecco un esempio di questa sintassi:
```js
const person = {
  name: "Taylor",
  sayHello() {
    return `Hello! My name is ${this.name}.`;
  }
};
```

---

## Usare la sintassi class per definire una funzione costruttore

ES6 fornisce una nuova sintassi per creare oggetti, utilizzando la parola chiave class (classe).

Va notato che la sintassi class è appunto solo una sintassi, e non la vera e propria implementazione basata su classi di un paradigma orientato agli oggetti, a differenza di quanto accade in linguaggi come Java, Python, Ruby, ecc.

In ES5, di solito definiamo una funzione constructor e usiamo la parola chiave new per istanziare un oggetto.
```js
var SpaceShuttle = function(targetPlanet){
  this.targetPlanet = targetPlanet;
}
var zeus = new SpaceShuttle('Jupiter
```

La sintassi class sostituisce semplicemente la creazione della funzione constructor:
```js
class SpaceShuttle {
  constructor(targetPlanet) {
    this.targetPlanet = targetPlanet;
  }
}
const zeus = new SpaceShuttle('Jupiter');
```
Va notato che la parola chiave class dichiara una nuova funzione, alla quale viene aggiunto un costruttore. Questo costruttore viene invocato quando new viene chiamata per creare un nuovo oggetto.

Nota: Per i nomi di classi ES6 dovrebbe essere usato per convenzione lo stile di scrittura UpperCamelCase, come fatto sopra in SpaceShuttle.

Il metodo costruttore constructor è un metodo speciale per creare e inizializzare un oggetto creato con class. Potrai approfondire la cosa nella sezione Programmazione Orientata agli Oggetti della certificazione Algoritmi e Strutture Dati in JavaScript.

---

## Usare getter e setter per controllare l'accesso a un oggetto

È possibile ottenere valori da un oggetto ed impostare il valore di una proprietà all'interno di un oggetto.

Queste due azioni sono classicamente chiamate getter e setter.

Le funzioni getter sono destinate semplicemente a restituire (to get, ottenere) all'utente il valore della variabile privata di un oggetto, senza che l'utente acceda direttamente alla variabile privata.

Le funzioni setter sono destinate a modificare (to set, impostare) il valore della variabile privata di un oggetto in base al valore passato nella funzione di impostazione. Questa modifica potrebbe comportare calcoli, o addirittura sovrascrivere completamente il valore precedente.
```js
class Book {
  constructor(author) {
    this._author = author;
  }
  // getter
  get writer() {
    return this._author;
  }
  // setter
  set writer(updatedAuthor) {
    this._author = updatedAuthor;
  }
}
const novel = new Book('anonymous');
console.log(novel.writer);
novel.writer = 'newAuthor';
console.log(novel.writer);
```
La console mostrerà le stringhe anonymous e newAuthor.

Notare la sintassi utilizzata per invocare le funzioni getter e setter. Non assomigliano nemmeno a funzioni. Getter e setter sono importanti perché nascondono i dettagli interni dell'implementazione.

Nota: È convenzione precedere il nome di una variabile privata con un underscore(_). Tuttavia, la pratica in sé non rende privata una variabile.

---

## Creare un modulo

JavaScript ha iniziato con un piccolo ruolo da giocare in un web fatto per lo di HTML. Oggi è enorme, e alcuni siti web sono costruiti quasi interamente con JavaScript. Per rendere JavaScript più modulare, pulito e mantenibile; ES6 ha introdotto un modo per condividere facilmente il codice tra i file JavaScript. Ciò comporta l'esportazione di parti di un file per l'utilizzo in uno o più altri file, e l'importazione delle parti di cui hai bisogno, dove ne hai bisogno. Per sfruttare questa funzionalità, devi creare uno script nel tuo documento HTML con un type di module. Ecco un esempio:
```js
<script type="module" src="filename.js"></script>
```
Uno script che utilizza questo tipo module può ora utilizzare le funzionalità di import e export che conoscerai nelle prossime sfide.

---

## Usare export per condividere un blocco di codice

Immagina un file chiamato math_functions.js che contiene diverse funzioni relative alle operazioni matematiche. Una di esse è memorizzata in una variabile, add, che prende due numeri e restituisce la loro somma. Vuoi utilizzare questa funzione in diversi file JavaScript. Per condividerlo con questi altri file, devi prima farne l'export.
```js
export const add = (x, y) => {
  return x + y;
}
```
Quanto sopra è un metodo comune per esportare una singola funzione, ma è possibile ottenere la stessa cosa in questo modo:
```js
const add = (x, y) => {
  return x + y;
}

export { add };
```
Quando si esporta una variabile o funzione, è possibile importarla in un altro file e usarla senza dover riscriverne il codice. È possibile esportare più cose ripetendo il primo esempio per ogni cosa che si desidera esportare, o inserendoli tutti nella dichiarazione di esportazione del secondo esempio, così:
```js
export { add, subtract };
```

---

## Riutilizzare codice JavaScript usando import

import ti permette di scegliere quali parti di un file o di un modulo caricare. Nella lezione precedente, gli esempi esportavano add dal file math_functions.js. Ecco come è possibile importarlo per usarlo in un altro file:

```js
import { add } from './math_functions.js';
```
Qui, import troverà add nel file math_functions.js, importerà solo quella funzione per il tuo utilizzo ed ignorerà il resto. Il ./ dice all'importazione di cercare il file math_functions.js nella stessa cartella del file attuale. Il percorso relativo del file (./) e l'estensione del file (.js) sono necessari quando si utilizza import in questo modo.

È possibile importare più di un elemento dal file aggiungendoli nell'istruzione import in questo modo:
```js
import { add, subtract } from './math_functions.js';
```

---

## Usare * per importare tutto da un file
Supponiamo di avere un file e di voler importare tutti i suoi contenuti nel file corrente. Questo può essere fatto con la sintassi import * as. Ecco un esempio in cui il contenuto di un file chiamato math_functions.js viene importato in un file nella stessa directory:
```js
import * as myMathModule from "./math_functions.js";
```
L'istruzione import di cui sopra creerà un oggetto chiamato myMathModule. Questo è solo un nome di variabile, puoi chiamarlo in qualsiasi modo. L'oggetto conterrà tutte le esportazioni di math_functions.js, così potrai accedere alle funzioni come faresti con qualsiasi altra proprietà di un oggetto. Ecco come utilizzare le funzioni add e subtract che sono state importate:
```js
myMathModule.add(2,3);
myMathModule.subtract(5,3);
```

--- 

## Creare un'esportazione predefinita con export default
Nella lezione sull'export, hai imparato a conoscere la sintassi indicata come esportazione con nome. Questo ti ha permesso di rendere disponibili più funzioni e variabili per l'utilizzo in altri file.

C'è un'altra sintassi export che devi conoscere, nota come export default (esportazione predefinita). Di solito si utilizza questa sintassi se un solo valore viene esportato da un file. Viene utilizzata anche per creare un valore di default per un file o un modulo.

Di seguito sono riportati esempi che utilizzano export default:
```js
export default function add(x, y) {
  return x + y;
}

export default function(x, y) {
  return x + y;
}
```
La prima è una funzione con un nome e la seconda è una funzione anonima.

Dato che export default è utilizzato per dichiarare un valore di default per un modulo o un file, si può avere un solo valore di esportazione predefinita in ogni modulo o file. Inoltre, non è possibile usare export default con var, let, o const

---

## Importare un'esportazione predefinita
Nell'ultima sfida, hai conosciuto l'esportazione predefinita (export default) e i suoi utilizzi. Per importare un'esportazione predefinita, è necessario utilizzare una diversa sintassi di import. Nell'esempio seguente, add è l'esportazione predefinita del file math_functions.js. Ecco come importarlo:
```js
import add from "./math_functions.js";
```
La sintassi differisce in un punto chiave. Il valore importato, add, non è circondato da parentesi graffe ({}). add qui è semplicemente il nome di una variabile per qualunque sia l'esportazione predefinita del file math_functions.js. È possibile utilizzare qualsiasi nome qui quando importi un valore predefinito.

---

## Creare una promise in JavaScript
Una promise (promessa) in JavaScript è esattamente quello che sembra - si usa per promettere di fare qualcosa, di solito in modo asincrono. Quando l'azione è completata, o adempi alla tua promessa o non riesci a farlo. Promise è una funzione costruttore, quindi è necessario utilizzare la parola chiave new per crearne una. Prende per argomento una funzione con due parametri - resolve e reject. Questi sono metodi utilizzati per determinare il risultato della promise. La sintassi si presenta così:
```js
const myPromise = new Promise((resolve, reject) => {

});
```

---

## Completare una promise con resolve e reject
Una promise ha tre stati: pending (in attesa), fulfilled (soddisfatta) e rejected (rifiutata). La promise che hai creato nell'ultima sfida è bloccata per sempre nello stato pending perché non hai aggiunto un modo per completarla. I parametri resolve e reject forniti all'argomento della promise vengono utilizzati per farlo. resolve è usato quando vuoi che la promise abbia successo, e reject è usato quando vuoi che la promise fallisca. Questi sono metodi che prendono un argomento, come si vede qui sotto.
```js
const myPromise = new Promise((resolve, reject) => {
  if(condition here) {
    resolve("Promise was fulfilled");
  } else {
    reject("Promise was rejected");
  }
});
```
L'esempio di cui sopra utilizza stringhe come argomento di queste funzioni, ma essi possono davvero essere qualsiasi cosa. Spesso potrebbe essere un oggetto, di cui potresti voler utilizzare i dati per metterli sul tuo sito web o altrove.

--- 

## Gestire una promise mantenuta con then
Le promise sono più utili quando hai nel codice un processo che richiede una quantità sconosciuta di tempo (cioè qualcosa di asincrono), spesso una richiesta al server. Quando si effettua una richiesta ad un server questa prende un certo lasso di tempo, e, dopo che si è conclusa, di solito si desidera fare qualcosa con la risposta del server. Questo risultato può essere ottenuto utilizzando il metodo then. Il metodo then viene eseguito immediatamente dopo che la promise è stata mantenuta con resolve. Ecco un esempio:
```js
myPromise.then(result => {

});
```
result deriva dall'argomento dato al metodo resolve.

--- 

## Gestire una promise rifiutata con catch
catch è il metodo utilizzato quando una promise è stata respinta. Viene eseguito immediatamente dopo che viene chiamato il metodo reject di una promise. Ecco la sintassi:
```js
myPromise.catch(error => {

});
```
error è l'argomento passato al metodo reject.

Aggiungi il metodo catch alla tua promise. Usa error come parametro della sua funzione di callback e scrivi error sulla console.
