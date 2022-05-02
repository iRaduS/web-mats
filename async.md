Metode de programare asincronică
================================

JavaScript ne oferă două metode prin care putem gestiona operațiile asincronice: callbacks și promises.

Callbacks
---------

Înainte de introducerea promise-urilor în JavaScript, singurul mod de realiza programare asincronică în JavaScript era folosind callbacks. Ideea este simplă: oferim în parametrii funcției ce va realiza o operație asincronică. Astfel, aceasta va apela funcția pe care i-am dat-o în momentul în care va termina operația. De obicei se oferă drept parametru două funcții - una în caz de succes și una în caz de eroare.

În exemplul de mai jos se prezintă o funcție ce simulează un apel către un API de vreme. Este important de reținut că la apelarea acesteia într-un bloc de cod nu se va aștepta terminarea execuției acesteia, codul statement-urile sincronice desfășurându-se în paralel cu aceasta.

Promises
--------

Adăugate în ES6 (2015), promise-urile sunt capabile să gestioneze mai ușor decât callback-urile programarea asincronă în JavaScript. Un promise ne "promite" că vom primi un rezultat sau o eroare la un moment dat. Acest obiect se poate găsi în trei faze:

*   _pending_ - starea inițială, nici îndeplinit nici rejectat;
*   _fullfilled_ - operația a fost executată cu succes;
*   _rejected_ - operația a suferit o eroare.

### Crearea de Promises

Fosind constructorul `Promise()` putem crea un nou obiect Promise. Modul de creare a promise-urilor este similar metodei callback-urilor:

**Sintaxă:**

*   `executor` - funcție cu 2 parametri
    *   `resolve` - funcție ce se apelează în cazul succesului, rezultatul fiind dat ca parametru
    *   `reject` - funcție ce se apelează în cazul erorii, eroarea fiind dată ca parametru

### Așteptarea rezultatului unui Promise

Folosim metodele și pentru a aștepa după îndeplinirea, respectiv rejectarea unui promise. Unul dintre avantajele promise-urilor este sintaxa mai simplă în modul de operare: metodele menționate mai sus returnează tot un promise, ceea ce ne permite să facem _chaining_. Ambele metode iau drept parametri funcții care vor fi executate la îndeplinirea/ rejectarea promise-ului.

### Metode statice

Așteaptă după rezolvarea tututor promise-urilor din `arr`, sau până când una este rejectată. În caz de succes, va returna promise ce are ca valoare un array cu valorile rezolvate. În caz de eșec, va returna un promise rejectat cu motivul primului promise unde a apărut eroarea.

Așteaptă după finalizarea (fie prin succes sau eșec) tututor promise-urilor din `arr`. Va returna un promise ce are ca valoare un array de forma .

Așteaptă după rezolvarea a uneia dintre promise-urile din `arr` și returnează un promise reprezentând promise-ul rezolvat primul.

Returnează un promise care este rejectat cu `reason`.

Returnează un promise care este rezolvat cu valoarea `value`.

### Metode pe instanță

Adaugă funcții callback pentru momentul în care promise-ul este finalizat: una pentru rezolvare și una opțională în caz de eroare. Poate fi îmlănțuit de mai multe ori.

Setează o funcție callback pentru momentul în care promise-ul este rejectat.

Adaugă o funcție callback pentru momentul în care promise-ul este finalizat. Rulează după cazurile de succes și eroare.

Funcții async/await
-------------------

Putem marca o funcție ca fiind `async` adăugând acest keyword înaintea declarării acesteia. Astfel vom putea avea acces la folosirea keyword-ului `await` în corpul acesteia. `await` ne permite să blocăm execuția codului în așteptarea rezolvării unui promise. Eventualele erori pot fi prinse folosind un bloc `try/catch`.

Funcțiile asincronice nu returnează un rezultat, ci un promise ce are ca valoare rezultatul respectiv!

Avantajul folosirii funcțiilor asincronice este că lucrul cu promise-uri devine mult mai ușor, scăpându-ne de așa-numitul _callback hell_. Presupunem în exemplul de mai jos că avem nevoie să obținem de la un server date despre utilizatorul autentificat, apoi pe baza acelor date vom face imediat un alt request către server.

Funcții de timeout și interval
==============================

În cazul în care dorim să executăm cod după un anume timp sau la un interval anume, JavaScript ne oferă funcții utilitare pentru acest lucru.

`setTimeout()`
--------------

**Sintaxă:**

Rulează funcția `handler` cu argumentele `...args` după `delay` milisecunde și returnează un ID al timeout-ului.

`setInterval()`
---------------

**Sintaxă:**

Rulează funcția `handler` cu argumentele `...args` o dată la `delay` milisecunde și returnează un ID al intervalului.

`clearTimeout()`
----------------

**Sintaxă:**

Anulează timeout-ul cu ID-ul `timeoutId` (dacă nu s-a terminat deja).

`clearInterval()`
-----------------

**Sintaxă:**

Anulează intervalul cu ID-ul `intervalId`.

Fetch API
=========

Pentru face cereri către un server și primi răspunsuri, JavaScript ne pune la dispoziție Fetch API.

Metoda `fetch()`
----------------

Metoda `fetch()` ne permite să cerem resurse de la server. Aceasta returnează un Promise care este rezolvat tot timpul, în afara cazurilor în care există o problemă de rețea. Astfel, un promise `fetch()` nu rejectează erorile HTTP (`404`, `403`, `500`, etc.). În schimb va trebui să verificăm în interiorul `then`\-ului dacă request-ul a fost finalizat cu succes.

**Sintaxă:** `fetch(resource, [, init])`

`resource`

URL-ul către resursa dorită.

`init`

Obiect ce conține diferite setări pe care dorim să le personalizăm. Acestea sunt:

`method`

Metoda HTTP a request-ului, de exemplu `GET` sau `POST`.

`headers`

Headere HTTP pe care dorim să le adăugăm la request. Valoarea poate fi de tip `Headers` sau un object literal cu valori String.

`body`

Body-ul request-ului. Poate fi un `Blob`, `FormData`, `String` etc.

`credentials`

Controlează ce face browser-ul cu datele credențiale (precum cookie-urile). Trebuie să fie unul dintre următoarele:

`omit`

Browser-ul va exclude credențialele din request și va ignora credențialele trimise înapoi în răspuns (de exemplu header-ul `Set-Cookie`).

`same-origin`

Browser-ul va trimite credențiale ce își au originea la același URL și va folosi credențialele trimise înapoi doar dacă au aceeași origine.

`include`

Browser-ul va trimite credențialele atât în request-uri same-origin cât și în cele cross-origin. Va folosi tot timpul credențialele trimise înapoi.

Interfața `Response`
--------------------

`Response` este un obiect care conține informații despre răspunsul serverului.

### Proprietăți

#### `body`

Returnează body-ul răspunsului.

#### `ok`

Returnează `true` dacă răspunsul a fost finalizat cu succes (coduri `2xx`).

#### `status`

Returnează codul răspunsului.

#### `url`

Returnează URL-ul răspunsului.

### Metode

#### `arrayBuffer()`

Returnează un promise ce se rezolvă într-un `ArrayBuffer` care conține datele răspunsului.

#### `blob()`

Returnează un promise ce se rezolvă într-un `Blob` care conține datele răspunsului.

#### `json()`

Returnează un promise ce se rezolvă cu rezultatul parcurgerii body-ului răspunsului ca JSON.

#### `text()`

Returnează un promise ce se rezolvă cu o reprezentare text a body-ului răspunsului.

Exemple
-------
```html
<form>
  Convertește
  <input type="number" name="amount" value="1" step="0.01"/>
  <select name="from" value="eur">
    <option value="eur">EUR</option>
    <option value="usd">USD</option>
    <option value="gbp">GBP</option>
    <option value="jpy">JPY</option>
    <option value="chf">CHF</option>
    <option value="ron">RON</option>
  </select>
  în
  <select name="to" value="usd">
    <option value="eur">EUR</option>
    <option value="usd" selected>USD</option>
    <option value="gbp">GBP</option>
    <option value="jpy">JPY</option>
    <option value="chf">CHF</option>
    <option value="ron">RON</option>
  </select>
  <input type="submit" value="Convertește"/>
</form>

<div id="result"></div>
```
```js
window.onload = () => {
  document.querySelector('form').addEventListener('submit', (event) => {
    event.preventDefault();
    covertCurrency();
  });
}

async function covertCurrency() {
  const form = document.querySelector('form');
  const formData = new FormData(form);
  const amount = parseFloat(formData.get('amount'));
  const fromCurrency = formData.get('from');
  const toCurrency = formData.get('to');
  const url = `https://cdn.jsdelivr.net/gh/fawazahmed0/currency-api@1/latest/currencies/${fromCurrency}/${toCurrency}.json`;
  document.querySelector('#result').innerHTML = 'Se încarcă...';
  try {
    const result = await fetch(url);
    const rate = await result.json();
    const convertedAmount = (amount * rate[toCurrency]).toFixed(2);
    document.querySelector('#result').innerHTML = `${amount} ${fromCurrency} = ${convertedAmount} ${toCurrency}`;
  } catch (error) {
    document.querySelector('#result').innerHTML = "A apărut o eroare!";
  }
}
```

Stocare
=======

JavaScript dispune de mai multe API-uri ce permit stocarea persistentă a datelor. Printre acestea se numără `localStorage`, `sessionStorage` și `indexedDB`.

LocalStorage
------------

`localStorage` permite stocarea datelor în browser-ul utilizatorului. Stocarea este locală, fiind accesibilă doar în browser-ul respectiv. Itemele sunt stocate sub forma unui tuplu cheie-valoare, ambele fiind de tip String. Astfel, în cazul în care dorim să obținem/setăm valoarea unui item ca obiect, trebuie să folosim metodele `JSON.parse()` și respectiv `JSON.stringify()`.

### Metode ale obiectului Storage

Folosind următoarele metode putem manipula datele stocate în `localStorage`.

#### `Storage.getItem(key)`

Returnează valoarea unui item cu cheia specificată.

#### `Storage.setItem(key, value)`

Setează valoarea `value` la cheia `key` în spațiul de stocare.

#### `Storage.removeItem(key)`

Elimină un item cu cheia specificată.

#### `Storage.clear()`

Elimină toate datele stocate în spațiul de stocare.
