# '#'  Ovo je H1

## '##' Ovo je H2

### '###' Ovo je H3

#### '####' Ovo je H4

##### '#####' Ovo je H5

###### '######' Ovo je H6

## Text features

Za **bold** tekst koristimo * *.

Za _italic_ tekst koristimo _ _.

Za ~~striked~~ tekst koristimo ~~ ~~.

## Links

Za linkove koristimo <https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet> tag <>.

Za [ovaj](http://github.com/Ninna994) tag koristimo kombinaciju '[] ()'.

Za slucaj da nam je dugacak [link][1] i da nam je tesko da se snadjemo smestamo umesto u obicne zagrade link u kockaste i unutra napisemo **key** koji ce nam biti definisam na kraju dokumenta sa key: pa vrednost.

Za [hover](http://github.com/Ninna994 "Ovo je hover.") koristimo samo " " posle linka u zagradama.

## Slike

Za slike se koristi !-slika je []-alternativno ime za screen readere ()-link do slike.

![Odlicna slika](http://unsplash.it/500/500?random "Random slika sa unsplash.it-a")

Umesto linka moze da stoji i definisan key kao u links.

![kuca][slika kuce]

### Da napravimo link do slike korstimo samo nested verziju

[![](http://unsplash.it/50/50?image=1000 "Link do slike")](http://unsplash.it/500/500?image=1000 "Random slika sa unsplash.it-a")

## Unordered List

Pravi se tako sto se ispred stavki stavi * ili + ili -

+ mleko
+ jogurt
+ hleb

## Ordered List

Pravi se tako sto se ispred stavke stavi 1., ako zelimo podstavku samo enter i indent i opet +*-ili 1.

1. mleko

   + dugotrajno
   + sveze
      + 2.8

1. hleb
1. jogurt

## Horizontal rule ---- ili ===

Nesto

---

Nesto drugo

## Blockquotes

> Ovo je rekao **Njutn**.
>
> A ovo je rekao **Njegos**.

## Code Blocks tri puta ` i na kraju isto . Na pocetku posle navoda stavi jezik koji je koristen

Here is my code:

```javascript
  var x = 100;
  const dog ='snickers';
```

Here is my php with mysql:

```php
  $query = mysqli_query($connection, "SELECT * FROM database_table");
```

Here is my java

```java
  System.out.println("Ovo je moj string koji se stampa");
```

Inline ga pisemo `var x = 100;`

Savet za ispravku sa diff + i -

```diff
- var y = 100;
+ var y = 150;
```

## Tabele |izmedju svakog imena kolone i svake stavke kolona. |:---:| u novom redu centrira tekst, mora se satviti za svaku stavku

|Name|Age|
|:---:|:--:|
|Snickers|2| |Prudence|8|

## Checkboxes se generisu kao [ ]  ime ili [x] ime

+ [x] mleko
+ [x] hleb
+ [ ] jogurt

[1]: http://github.com/Ninna994
[slika kuce]: http://unsplash.it/500/500?image=1012
