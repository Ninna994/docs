# JavaScriptDOM CheatSheet

## by Ninna

### Table of Contents

- [JavaScriptDOM CheatSheet](#javascriptdom-cheatsheet)
  - [by Ninna](#by-ninna)
    - [Table of Contents](#table-of-contents)
    - [Intro](#intro)
    - [Math functions](#math-functions)
    - [Document functions](#document-functions)
    - [Events](#events)

### Intro

1. **DOM** is Document Object Model- Structured respresentation of an HTML document

### Math functions

1. Math.**floor()** - zaokruzuje broj
1. Math.**random()** - vraca random broj od 0-1, ako zelimo random broj neki drugi izmedju neka dva broja koristimo  _floor(random*broj_koji_treba)_. Da izuzmemo 0 samo dodamo + 1;

### Document functions

1. **querySelector('.name, #name, element')** -vraca _prvi element_ koji se podudara sa selektorom koji je trazen. Moze se koristiti i kao setter i kao getter.
1. **getElementByID('name)** - brze nego query selector
1. **.textContent** - dozvoljava upisivanje samo prostog teksta

   ```JavaScript
    document.querySelector('id').textContent = biloSta;
   ```

1. **innerHTML** - dozvoljava upisivanje html elementa

   ```JavaScript
    document.querySelector('id').innerHTML = '<h1>' + vrednost + '</h1>';
   ```

1. **.style** - za manipulisanje css-om.

   ```JavaScript
    document.querySelector('id').style.property ='value' ;
   ```

1. **.classList** za manipulisanje klasama
   * add
   * remove
   * toggle

1.**Anonimne** funkcije su funkcije koje nemaju ime i  ne mozemo da koristimo iznova i one se nalaze uglavnom unutar event listenera kao drugi argument. Ako zelimo da ih opet koristimo ispisemo ih van listenera i pozovemo ih bez ()
unutar njega.

### Events

1. Obavestavaju kod da se nesto desilo sa stranicom. Trigeruju se sa klikom, skrolom, klikom dugmeta itd. Koristimo **event listener** da sprovedemo neku akciju u odnosu na to koji se event desio. _Event listener_ ceka da se desi neka radnja da bi se pokrenuo.

1.Sintaksa

   ```JavaScript
    document.querySelector('id').addEventListener('event', function(){
      //do something
    }) ;
   ```
