# Programmazione Orientata agli Oggetti

## Creare un semplice oggetto JavaScript
Pensa alle cose che la gente vede ogni giorno, come automobili, negozi e uccelli. Queste sono tutti oggetti (objects): cose tangibili che le persone possono osservare e con cui possono interagire.

Quali sono alcune caratteristiche di questi oggetti? Un'automobile ha delle ruote. I negozi vendono oggetti. Gli uccelli hanno le ali.

Queste caratteristiche, o proprietà, definiscono ciò che costituisce un oggetto. Nota che oggetti simili condividono le stesse proprietà, ma possono avere valori diversi per quelle proprietà. Per esempio, tutte le automobili hanno ruote, ma non tutte le automobili hanno lo stesso numero di ruote.

Gli oggetti in JavaScript sono utilizzati per modellare oggetti del mondo reale, dando loro proprietà e comportamenti proprio come le loro controparti del mondo reale. Ecco un esempio che utilizza questi concetti per creare un oggetto duck (anatra):
```js
let duck = {
  name: "Aflac",
  numLegs: 2
};
```
Questo oggetto duck ha due coppie proprietà/valore: un name di Aflac e un numLegs (numero di zampe) di 2.

---

## Usare la notazione a punti per accedere alle proprietà di un oggetto
L'ultima sfida ha creato un oggetto con varie proprietà. Ora vedrai come accedere ai valori di queste proprietà. Ecco un esempio:
```js
let duck = {
  name: "Aflac",
  numLegs: 2
};
console.log(duck.name);
```
La notazione a punti è usata sul nome dell'oggetto, duck, seguita dal nome della proprietà, name, per accedere al valore Aflac.

--- 

## Creare un metodo per un oggetto
Gli oggetti possono avere un tipo speciale di proprietà, chiamato metodo.

I metodi sono proprietà che sono funzioni. Questo aggiunge comportamenti diversi a un oggetto. Ecco l'esempio di duck con un metodo:
```js
let duck = {
  name: "Aflac",
  numLegs: 2,
  sayName: function() {return "The name of this duck is " + duck.name + ".";}
};
duck.sayName();
```
L'esempio aggiunge il metodo sayName, che è una funzione che restituisce una frase con il nome dell'anatra (duck). Nota che il metodo ha avuto accesso alla proprietà name nell'istruzione return utilizzando duck.name. La prossima sfida mostrerà un altro modo per farlo.

---

## Rendere il codice più riutilizzabile con la parola chiave this
L'ultima sfida ha introdotto un metodo nell'oggetto duck. Ha usato la notazione a punti duck.name per accedere al valore per la proprietà name all'interno dell'istruzione return:
```js
sayName: function() {return "The name of this duck is " + duck.name + ".";}
```
Anche se questo è un modo valido per accedere alla proprietà dell'oggetto, c'è una trappola... Se il nome della variabile cambia, anche qualsiasi porzione di programma che si riferisca al nome originale dovrebbe essere aggiornato. In una definizione dell'oggetto breve, questo non sarà un problema, ma se un oggetto ha molti riferimenti alle sue proprietà ci sarà una maggiore probabilità di errore.

Un modo per evitare questi problemi è con la parola chiave this:
```js
let duck = {
  name: "Aflac",
  numLegs: 2,
  sayName: function() {return "The name of this duck is " + this.name + ".";}
};
```
this è un concetto profondo, e l'esempio di cui sopra è solo un modo per usarlo. Nel contesto corrente, this si riferisce all'oggetto a cui il metodo è associato: duck. Se il nome dell'oggetto viene cambiato in mallard, non sarà necessario trovare tutti i riferimenti a duck nel codice. Questo rende il codice riutilizzabile e più facile da leggere.

---

## Definire una funzione costruttore
I costruttori sono funzioni che creano nuovi oggetti. Essi definiscono proprietà e comportamenti che appartengono al nuovo oggetto. Pensa ad essi come a progetti per la creazione di nuovi oggetti.

Ecco un esempio di costruttore:
```js
function Bird() {
  this.name = "Albert";
  this.color = "blue";
  this.numLegs = 2;
}
```
Questo costruttore definisce un oggetto Bird con proprietà name, color, e numLegs impostati rispettivamente su Albert, blue e 2. I costruttori seguono alcune convenzioni:

- I costruttori sono definiti con un nome con l'iniziale maiuscola per distinguerli dalle altre funzioni che non sono costruttori (constructors).
- I costruttori usano la parola chiave this per impostare le proprietà dell'oggetto che creeranno. All'interno del costruttore, this si riferisce al nuovo oggetto che creerà.
- I costruttori definiscono proprietà e comportamenti invece di restituire un valore come fanno le normali funzioni.

---

## Usare un costruttore per creare oggetti
Ecco il costruttore di Bird della sfida precedente:
```js
function Bird() {
  this.name = "Albert";
  this.color  = "blue";
  this.numLegs = 2;
}

let blueBird = new Bird();
```
NOTA: this all'interno del costruttore si riferisce sempre all'oggetto che viene creato.

Nota che l'operatore new viene utilizzato per chiamare un costruttore. Questo dice a JavaScript di creare una nuova istanza di Bird chiamata blueBird. Senza l'operatore new, this all'interno del costruttore non punterebbe all'oggetto appena creato, dando risultati inattesi. Ora blueBird ha tutte le proprietà definite all'interno del costruttore Bird:
```js
blueBird.name;
blueBird.color;
blueBird.numLegs;
```
Proprio come qualsiasi altro oggetto, le sue proprietà sono accessibili e possono essere modificate:
```js
blueBird.name = 'Elvira';
blueBird.name;
```

--- 

## Estendere i costruttori facendogli ricevere argomenti
I costruttori Bird e Dog dell'ultima sfida hanno funzionato bene. Tuttavia, nota che tutti i Birds che vengono creati con il costruttore Bird sono automaticamente chiamati Albert, sono di colore blu e hanno due zampe. E se volessi degli uccelli con valori diversi per nome e colore? È possibile cambiare manualmente le proprietà di ogni uccello, ma questo sarebbe molto laborioso:
```js
let swan = new Bird();
swan.name = "Carlos";
swan.color = "white";
```
Supponi di voler scrivere un programma per tenere traccia di centinaia o addirittura migliaia di uccelli diversi in una voliera. Ci vorrebbe molto tempo per creare tutti gli uccelli e successivamente cambiare le proprietà impostando valori diversi per tutti. Per creare più facilmente diversi oggetti Bird, puoi progettare il tuo costruttore Bird in modo che accetti dei parametri:
```js
function Bird(name, color) {
  this.name = name;
  this.color = color;
  this.numLegs = 2;
}
```
Potrai quindi passargli dei valori come argomenti al costruttore Bird per definire ogni singolo uccello: let cardinal = new Bird("Bruce", "red"); crea una nuova istanza di Bird con le proprietà name e color impostate rispettivamente a Bruce e red. La proprietà numLegs è ancora impostata a 2. Il cardinal ha queste proprietà:
```js
cardinal.name
cardinal.color
cardinal.numLegs
```
Il costruttore è più flessibile. Ora è possibile definire le proprietà per ogni Bird al momento della creazione, che è uno dei motivi per cui i costruttori JavaScript sono così utili. Essi raggruppano gli oggetti in base a caratteristiche e comportamenti condivisi e definiscono un progetto che automatizza la loro creazione.

---

## Verificare il costruttore di un oggetto con instanceof
Ogni volta che una funzione costruttore crea un nuovo oggetto, si dice che l'oggetto è un'istanza del suo costruttore. JavaScript offre un modo conveniente per verificarlo con l'operatore instanceof. instanceof ti permette di confrontare un oggetto con un costruttore, restituendo true o false in base al fatto che l'oggetto sia stato creato o meno con quel costruttore. Ecco un esempio:
```js
let Bird = function(name, color) {
  this.name = name;
  this.color = color;
  this.numLegs = 2;
}

let crow = new Bird("Alexis", "black");

crow instanceof Bird;
```
Questo metodo instanceof restituirà true.

Se un oggetto viene creato senza usare un costruttore, instanceof verificherà che non si tratta di un'istanza di quel costruttore:
```js
let canary = {
  name: "Mildred",
  color: "Yellow",
  numLegs: 2
};

canary instanceof Bird;
```
Questo metodo instanceof restituirà false.

---

## Comprendere le proprietà proprie
Nell'esempio seguente, il costruttore di Bird definisce due proprietà: name e numLegs:
```js
function Bird(name) {
  this.name = name;
  this.numLegs = 2;
}

let duck = new Bird("Donald");
let canary = new Bird("Tweety");
```
name e numLegs sono chiamati proprietà proprie, perché sono definite direttamente nell'oggetto istanza. Questo significa che sia duck che canary hanno la propria copia separata di queste proprietà. Di fatto ogni istanza di Bird avrà la propria copia di queste proprietà. Il seguente codice aggiunge tutte le proprietà proprie di duck all'array ownProps:
```js
let ownProps = [];

for (let property in duck) {
  if(duck.hasOwnProperty(property)) {
    ownProps.push(property);
  }
}

console.log(ownProps);
```
La console visualizzerà il valore ["name", "numLegs"].

---

## Usare le proprietà di Prototype per ridurre il codice duplicato
Poiché numLegs avrà probabilmente lo stesso valore per tutte le istanze di Bird, hai essenzialmente una variabile duplicata numLegs all'interno di ogni istanza di Bird.

Può non essere un problema se ci sono solo due istanze, ma immagina se ce ne fossero milioni! Sarebbe un sacco di variabili duplicate.

Un modo migliore è quello di utilizzare il prototype di Bird. Le proprietà del prototype sono condivise tra TUTTE le istanze di Bird. Ecco come aggiungere numLegs al Bird prototype:
```js
Bird.prototype.numLegs = 2;
```
Ora tutte le istanze di Bird hanno la proprietà numLegs.
```js
console.log(duck.numLegs);
console.log(canary.numLegs);
```
Dal momento che tutte le istanze hanno automaticamente le proprietà del prototype, pensa a un prototype come una "ricetta" per creare oggetti. Nota che il prototype per duck e per canary fa parte del costruttore Bird come Bird.prototype. Quasi ogni oggetto in JavaScript ha una proprietà prototype che fa parte della funzione costruttore che lo ha creato.

--- 

## Iterare fra tutte le proprietà
Ora hai visto due tipi di proprietà: proprietà proprie e proprietà di prototipo (prototype). Le proprietà proprie sono definite direttamente nell'istanza dell'oggetto. E le proprietà di prototipo sono definite nel prototype.
```js
function Bird(name) {
  this.name = name;  //own property
}

Bird.prototype.numLegs = 2; // prototype property

let duck = new Bird("Donald");
```
Ecco come aggiungere le proprietà di duck all'array ownProps e le proprietà di prototype all'array prototypeProps:
```js
let ownProps = [];
let prototypeProps = [];

for (let property in duck) {
  if(duck.hasOwnProperty(property)) {
    ownProps.push(property);
  } else {
    prototypeProps.push(property);
  }
}

console.log(ownProps);
console.log(prototypeProps);
```
console.log(ownProps) visualizzerà ["name"] nella console e console.log(prototypeProps) visualizzerà ["numLegs"].

--- 

## Comprendere la proprietà Costruttore
C'è una proprietà speciale constructor situata nelle istanze oggetto duck e beagle che sono state create nelle sfide precedenti:
```js
let duck = new Bird();
let beagle = new Dog();

console.log(duck.constructor === Bird); 
console.log(beagle.constructor === Dog);
```
Entrambe queste chiamate a console.log visualizzeranno true nella console.

Nota che la proprietà constructor è un riferimento alla funzione costruttore che ha creato l'istanza. Il vantaggio della proprietà constructor è che è possibile controllare questa proprietà per scoprire di che tipo di oggetto si tratta. Ecco un esempio di come usarlo:
```js
function joinBirdFraternity(candidate) {
  if (candidate.constructor === Bird) {
    return true;
  } else {
    return false;
  }
}
```
Nota: Poiché la proprietà constructor può essere sovrascritta (come vedremo nelle prossime due sfide) normalmente è meglio utilizzare il metodo instanceof per controllare il tipo di un oggetto.

---

## Cambiare il prototipo in un nuovo oggetto
Fino ad ora hai aggiunto singole proprietà al prototype:
```js
Bird.prototype.numLegs = 2;
```
Questo diventa noioso se hai un certo numero di proprietà.
```js
Bird.prototype.eat = function() {
  console.log("nom nom nom");
}

Bird.prototype.describe = function() {
  console.log("My name is " + this.name);
}
```
Un modo più efficiente è quello di impostare il prototype su un nuovo oggetto che contenga già le proprietà. In questo modo, le proprietà vengono aggiunte tutte contemporaneamente:
```js
Bird.prototype = {
  numLegs: 2, 
  eat: function() {
    console.log("nom nom nom");
  },
  describe: function() {
    console.log("My name is " + this.name);
  }
};
```

---

## Impostare la proprietà Costruttore quando si cambia il prototipo
C'è un effetto collaterale cruciale quando si imposta manualmente il prototipo su un nuovo oggetto. Questo cancella la proprietà constructor! Questa proprietà può essere utilizzata per verificare quale funzione costruttore ha creato l'istanza, ma poiché la proprietà è stata sovrascritta, ora dà come risultato false:
```js
duck.constructor === Bird;
duck.constructor === Object;
duck instanceof Bird;
```
Nell'ordine, queste espressioni restituiscono false,true e true.

Per risolvere questo problema, ogni volta che imposti manualmente un prototipo su un nuovo oggetto, ricorda di definire la proprietà constructor:
```js
Bird.prototype = {
  constructor: Bird,
  numLegs: 2,
  eat: function() {
    console.log("nom nom nom");
  },
  describe: function() {
    console.log("My name is " + this.name); 
  }
};
```

--- 

## Capire da dove viene il prototipo di un oggetto
Proprio come le persone ereditano i geni dai loro genitori, un oggetto eredita il suo prototype direttamente dalla funzione costruttore che lo ha creato. Ad esempio, qui il costruttore Bird crea l'oggetto duck:
```js
function Bird(name) {
  this.name = name;
}

let duck = new Bird("Donald");
```
duck eredita il suo prototype dalla funzione costruttore di Bird. Puoi mostrare questa relazione con il metodo isPrototypeOf:
```js
Bird.prototype.isPrototypeOf(duck);
```
Questo restituirà true.

---

## Comprendere la catena dei prototipi
Tutti gli oggetti in JavaScript (con alcune eccezioni) hanno un prototype. Inoltre, il prototype di un oggetto è esso stesso un oggetto.
```js
function Bird(name) {
  this.name = name;
}

typeof Bird.prototype;
```
Poiché un prototype è un oggetto, un prototype può avere il proprio prototype! In questo caso, il prototype di Bird.prototype è Object.prototype:
```js
Object.prototype.isPrototypeOf(Bird.prototype);
```
Come può esserti utile questo? Ricorderai il metodo hasOwnProperty da una sfida precedente:
```js
let duck = new Bird("Donald");
duck.hasOwnProperty("name");
```
Il metodo hasOwnProperty è definito in Object.prototype, a cui è possibile accedere da Bird.prototype, al quale si può a sua volta accedere da duck. Questo è un esempio della catena dei prototype. In questa catena di prototype, Bird è il supertype di duck, mentre duck è il subtype. Object è un supertype sia di Bird che di duck. Object è un supertype per tutti gli oggetti in JavaScript. Pertanto, qualsiasi oggetto può utilizzare il metodo hasOwnProperty.

---

## Usare l'ereditarietà per non ripeterti
C'è un principio nella programmazione chiamato Don't Repeat Yourself (DRY), che significa "non ripetere te stesso". Il motivo per cui il codice ripetuto è un problema è che qualsiasi modifica richiede di sistemare il codice in più punti. Questo di solito significa più lavoro per i programmatori e più spazio per gli errori.

Nota nell'esempio sottostante che il metodo describe è condiviso da Bird e da Dog:
```js
Bird.prototype = {
  constructor: Bird,
  describe: function() {
    console.log("My name is " + this.name);
  }
};

Dog.prototype = {
  constructor: Dog,
  describe: function() {
    console.log("My name is " + this.name);
  }
};
```
Il metodo describe viene ripetuto in due punti. Il codice può essere modificato per seguire il principio DRY creando un supertype (o genitore) chiamato Animal:
```js
function Animal() { };

Animal.prototype = {
  constructor: Animal, 
  describe: function() {
    console.log("My name is " + this.name);
  }
};
```
Dal momento che Animal include il metodo describe, puoi rimuoverlo da Bird e Dog:
```js
Bird.prototype = {
  constructor: Bird
};

Dog.prototype = {
  constructor: Dog
};
```

--- 

## Ereditare comportamenti da un Supertipo
Nella sfida precedente, hai creato un supertype chiamato Animal che definiva i comportamenti condivisi da tutti gli animali:
```js
function Animal() { }
Animal.prototype.eat = function() {
  console.log("nom nom nom");
};
```
Questa e la prossima sfida mostreranno come riutilizzare i metodi di Animal all'interno di Bird e Dog senza definirli nuovamente. Useremo una tecnica chiamata ereditarietà (inheritance). Questa sfida riguarda il primo passo: creare un'istanza del supertype (o genitore). Conosci già un modo per creare un'istanza di Animal utilizzando l'operatore new:
```js
let animal = new Animal();
```
Ci sono alcuni svantaggi quando si utilizza questa sintassi per l'ereditarietà, che è troppo complessa per questa sfida. Ecco invece un approccio alternativo senza questi svantaggi:
```js
let animal = Object.create(Animal.prototype);
```
Object.create(obj) crea un nuovo oggetto e imposta obj come suo prototype. Ricorda che il prototype è come la "ricetta" per creare un oggetto. Impostando il prototype di animal al prototype di Animal, stai di fatto dando all'istanza animal la stessa "ricetta" di qualsiasi altra istanza di Animal.
```js
animal.eat();
animal instanceof Animal;
```
Il metodo instanceof qui restituirebbe true.

---

## Impostare il prototipo del figlio su un'istanza del genitore
Nella sfida precedente hai visto il primo passo per ereditare il comportamento dal supertipo (o genitore) Animal: creare una nuova istanza di Animal.

Questa sfida copre la fase successiva: impostare il prototype del sottotipo (o figlio) — in questo caso Bird— in modo che sia un'istanza di Animal.
```js
Bird.prototype = Object.create(Animal.prototype);
```
Ricorda che il prototype è come la "ricetta" per creare un oggetto. In un certo senso, la ricetta per Bird ora include tutti gli "ingredienti" chiave di Animal.
```js
let duck = new Bird("Donald");
duck.eat();
```
duck eredita tutte le proprietà di Animal, compreso il metodo eat.

---

## Ripristinare una proprietà constructor ereditata
Quando un oggetto eredita il suo prototype da un altro oggetto, eredita anche la proprietà costruttore del supertipo.

Ecco un esempio:
```js
function Bird() { }
Bird.prototype = Object.create(Animal.prototype);
let duck = new Bird();
duck.constructor
```
Ma duck e tutte le istanze di Bird dovrebbero mostrare che sono stati costruiti da Bird e non da Animal. Per farlo, puoi impostare manualmente la proprietà costruttore di Bird all'oggetto Bird:
```js
Bird.prototype.constructor = Bird;
duck.constructor
```

---

## Aggiungere dei metodi a quelli ereditati
Una funzione costruttore che eredita il suo oggetto prototype da una funzione costruttore di supertipo può avere i propri metodi in aggiunta ai quelli ereditati.

Per esempio, Bird è un costruttore che eredita il suo prototype da Animal:
```js
function Animal() { }
Animal.prototype.eat = function() {
  console.log("nom nom nom");
};
function Bird() { }
Bird.prototype = Object.create(Animal.prototype);
Bird.prototype.constructor = Bird;
```
In aggiunta a quello che è ereditato da Animal, vuoi aggiungere un comportamento che sia unico per gli oggetti Bird. Qui, Bird riceverà una funzione fly(). Le funzioni vengono aggiunte al prototype di Bird allo stesso modo di qualsiasi funzione del costruttore:
```js
Bird.prototype.fly = function() {
  console.log("I'm flying!");
};
```
Ora le istanze di Bird avranno entrambi i metodi eat() e fly():
```js
let duck = new Bird();
duck.eat();
duck.fly();
```
duck.eat() visualizzerà nella console la stringa nom nom nom e duck.fly() mostrerà la stringa I'm flying!.

---

## Sovrascrivere metodi ereditati
Nelle lezioni precedenti, hai imparato che un oggetto può ereditare il suo comportamento (i metodi) da un altro oggetto facendo riferimento al suo oggetto prototype:

ChildObject.prototype = Object.create(ParentObject.prototype);
Quindi il ChildObject ha ricevuto i propri metodi concatenandoli a quelli del suo prototype:
```js
ChildObject.prototype.methodName = function() {...};
```
È possibile sovrascrivere un metodo ereditato. Lo si fa nello stesso modo: aggiungendo un metodo a ChildObject.prototype usando lo stesso nome di metodo di quello da sovrascrivere. Ecco un esempio di Bird che sovrascrive il metodo eat() ereditato da Animal:
```js
function Animal() { }
Animal.prototype.eat = function() {
  return "nom nom nom";
};
function Bird() { }

Bird.prototype = Object.create(Animal.prototype);

Bird.prototype.eat = function() {
  return "peck peck peck";
};
```
Se hai un'istanza let duck = new Bird(); e chiami duck.eat(), ecco come JavaScript cerca il metodo nella catena del prototype di duck:

1) duck => eat() è definito qui? No.
2) Bird => eat() è definito qui? => Sì. Eseguilo e smetti di cercare.
3) Animal => anche qui è definito eat(), ma JavaScript ha smesso di cercare prima di raggiungere questo livello.
4) Object => JavaScript ha smesso di cercare prima di raggiungere questo livello.

---

## Usare un Mixin per aggiungere un comportamento comune tra oggetti non correlati
Come hai visto, il comportamento è condiviso attraverso l'ereditarietà. Tuttavia, ci sono casi in cui l'ereditarietà non è la soluzione migliore. L'ereditarietà non funziona bene per oggetti non correlati come Bird e Airplane. Entrambi possono volare, ma un Bird non è un tipo di Airplane e viceversa.

Per gli oggetti non correlati, è meglio utilizzare i mixin. Un mixin permette ad altri oggetti di utilizzare una raccolta di funzioni.
```js
let flyMixin = function(obj) {
  obj.fly = function() {
    console.log("Flying, wooosh!");
  }
};
```
flyMixin prende qualsiasi oggetto e gli dà il metodo fly.
```js
let bird = {
  name: "Donald",
  numLegs: 2
};

let plane = {
  model: "777",
  numPassengers: 524
};

flyMixin(bird);
flyMixin(plane);
```
Qui bird e plane sono passati a flyMixin, che assegna la funzione fly ad entrambi. Ora bird e plane possono entrambi volare:
```js
bird.fly();
plane.fly();
```
La console visualizzerà la stringa Flying, wooosh! due volte, una volta per ogni chiamata di .fly().

Nota come il mixin permette di riutilizzare lo stesso metodo fly agli oggetti non correlati bird e plane.

--- 

## Usare le closure per proteggere da modifiche esterne le proprietà di un oggetto
Nella sfida precedente, bird aveva una proprietà pubblica name. È considerata pubblica perché può essere consultata e modificata dal di fuori della definizione di bird.
```js
bird.name = "Duffy";
```
Pertanto, qualsiasi parte del tuo codice può facilmente cambiare il nome di bird impostandolo a qualsiasi valore. Pensa a cosa succederebbe se cise come password e conti bancari fossero facilmente modificabili da qualsiasi parte del tuo codice. Questo potrebbe causare un sacco di problemi.

Il modo più semplice per rendere privata questa proprietà pubblica è quello di creare una variabile all'interno della funzione costruttore. Questo fa in modo che il campo di applicazione di questa variabile sia solo quello interno alla funzione costruttore, e non la rende più disponibile a livello globale. In questo modo, la variabile può essere consultata e modificata solo da metodi che siano anch'essi all'interno della funzione costruttore.
```js
function Bird() {
  let hatchedEgg = 10;

  this.getHatchedEggCount = function() { 
    return hatchedEgg;
  };
}
let ducky = new Bird();
ducky.getHatchedEggCount();
```
getHatchedEggCount è un metodo privilegiato, perché ha accesso alla variabile privata hatchedEgg. Questo è possibile perché hatchedEgg è dichiarato nello stesso contesto di getHatchedEggCount. In JavaScript, una funzione ha sempre accesso al contesto in cui è stata creata. Questa si chiama closure (chiusura).

---

## Comprendere l'espressione di funzione invocata immediatamente (IIFE)
Un modello comune in JavaScript è quello di eseguire una funzione non appena viene dichiarata:
```js
(function () {
  console.log("Chirp, chirp!");
})();
```
Questa è un'espressione di funzione anonima che viene eseguita subito, e produce Chirp, chirp! immediatamente.

Nota che la funzione non ha un nome e non è memorizzata in una variabile. Le due parentesi () alla fine dell'espressione della funzione fanno sì che essa sia immediatamente eseguita o invocata. Questo modello è conosciuto come una espressione funzione invocata immediatamente o IIFE.

---

## Usare una IIFE per creare un modulo
Un'espressione di funzione invocata immediatamente (IIFE) viene spesso usata per raggruppare le funzionalità correlate in un singolo oggetto o modulo. Per esempio, una sfida precedente ha definito due mixin:
```js
function glideMixin(obj) {
  obj.glide = function() {
    console.log("Gliding on the water");
  };
}
function flyMixin(obj) {
  obj.fly = function() {
    console.log("Flying, wooosh!");
  };
}
```
Possiamo raggruppare questi mixin in un modulo come segue:
```js
let motionModule = (function () {
  return {
    glideMixin: function(obj) {
      obj.glide = function() {
        console.log("Gliding on the water");
      };
    },
    flyMixin: function(obj) {
      obj.fly = function() {
        console.log("Flying, wooosh!");
      };
    }
  }
})();
```
Nota che hai un'espressione di funzione invocata immediatamente (IIFE) che restituisce un oggetto motionModule. L'oggetto restituito contiene tutti i comportamenti mixin come proprietà dell'oggetto. Il vantaggio del modello dei moduli è che tutti i comportamenti di movimento possono essere impacchettati in un singolo oggetto che può essere utilizzato da altre parti del codice. Ecco un esempio che lo utilizza:
```js
motionModule.glideMixin(duck);
duck.glide();
```