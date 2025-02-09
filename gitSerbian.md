# Uputstvo za korisćenje GIT-a

## Sadržaj

<!-- TOC -->

- [Uputstvo za korisćenje GIT-a](#uputstvo-za-korisćenje-git-a)
  - [Sadržaj](#sadržaj)
  - [Šta je GIT](#šta-je-git)
  - [Funkcionalnosti GIT-a](#funkcionalnosti-git-a)
  - [Instalacija GIT-a](#instalacija-git-a)
  - [Životni ciklus jednog repozitorijuma](#životni-ciklus-jednog-repozitorijuma)
  - [Komande za terminal GitBash](#komande-za-terminal-gitbash)
  - [Komande za git](#komande-za-git)
  - [.gitignore](#gitignore)
  - [Dodavanje SSH](#dodavanje-ssh)
  - [Remote push na repozitorijum](#remote-push-na-repozitorijum)
  - [Git za testing](#git-za-testing)

<!-- TOC End -->

## Šta je GIT

Git je **Version control** sistem za praćenje promena na računarskim fajlovima i za koordinisani rad više ljudi. Uglavnom se koristi za verzionisanje. Git je distribuirani sistem kontrole verzija.

Svaki GIT radni direktorijum na svakom računaru predstavlja kompletan **repozitorijum** sa kompletnom istorijom i upotpunjenom mogućnosti za praćenje verzija nezavisno od pristupa mreži ili centralnog servera.

## Funkcionalnosti GIT-a

1. GIT pravi **snapshot**-ove verzija, a ne samo specifičnih fajlova
1. **Repozitorijum** sadrži fajlove, istoriju, konfiguraciju
1. **Commit**
   * Sačuvana promena na git repozitorijumu
   * Svaki commit utiče na history tog repozitorijuma
   * Svaki commit ima jedinstven SHA1 hash koji mu služi za identifikaciju
1. **Remote hosting** provajderi služe za čuvanje repozitorijuma na serveru
   * GitHub
   * GitLab
   * BitBucket
1. **Branches** (grane) služe kao timeline commit-ova
   * glavna grana je master, default grana
1. **HEAD** je pokazivać na poslednji commit na grani
1. **Remote** je ne-lokalni repozitorijum koji je uvezan sa lokalnim repozitorijumom

## Instalacija GIT-a

1. Instalacija za **Windows**
   * Otići na [ovaj sajt](https://git-scm.com/downloads)
   * Skine se verzija gita koja odgovara sistemu računara(potrebne su dozvole na računaru)
   * Instalacijom se bira i default editor koji će se koristiti za GIT, defaultni je nano editor
   * Instalacija za običnog usera se  vrši preuzimanjem predloženih podešavanja bez menjanja kroz instalacioni meni
   * Pokretanjem GitBash terminala startuje se git okruženje
1. Instalacija za **MAC**
   * Ukoliko postoji na računaru instaliran _Xcode_ nije potrebno konfigurisati git jer je ugradjen
   * Za ostale pratiti uputstva za instalaciju Windows verzije samo odabrati verziju za MAC na početku
1. Nakon instalacije na oba uredjaja proveriti da li je git instaliran kako treba kucanjem komande

   ```git
    git version
   ```

## Životni ciklus jednog repozitorijuma

1. Local pristup -> Pravimo folder na našem računaru i vršimo postavljanje istog na remote server

   ```git
    konfigurisati git lokalno
    init
    work
    add
    commit
    push
    pull

   ```

1. Remote pristup -: Inicijalizujemo git na hosting provajderu i skidamo repozitorijum na lokalnu mašinu

   ```git
    init na hosting provajderu
    clone na lokal
    work
    add
    commit
    push
    pull

   ```

## Komande za terminal GitBash

1. _pwd_  -> u kom se folderu nalazimo
1. _exit_ -> izlaz iz terminala
1. _clear_  -> brisanje prethodnih komandi i rezultata iz terminala
1. _cd lokacija_ -> change directory (promeni direktorijum)
1. _cd ~_ -> odlazak na root folder
1. _cd .._ -> povratak na jedan folder iznad trenutnog foldera
1. _md naziv_ -> make directory (napravi direktorijum)
1. _ls_ -> sta se trenutno nalazi u folderu u kom se nalazimo
1. _cat fajl_ -> čitanje sadržaja nekog fajla
1. _code ime-fajla_ -> otvaranje fajla u VSCode

## Komande za git

1. _git version_ -> proverava da li je instaliran git u terminalu i koja se verzija koristi
1. _git help_ -> prikaz svih komandi
1. _git help komanda_ -> prikaz svih komandi koje se mogu kombinovati sa unesenom komandom
1. _git config --global user.name "username"_ -> konfigurisanje globalnog usera za git(uneti svoj username)
1. _git config --global user.email "email"_ -> konfigurisanje globalnog email-a za git(uneti svoj email)
1. _git config --global --list_ -> prikaz svih podataka koji su globalni i definisani
1. _git init projekat_ -> inicijaliyovanje git foldera i fajlova. Ukoliko se ne unese projekat git ce se inicijaliyovati na ternutnom folderu
1. _git clone "link"_ -> kloniranje postojeceg fajla sa remote hostinga na nas racunar
1. _git add ime-fajla_ -> dodavanje izmenjenog fajla na git
1. _git add ._ -> dodavanje svih izmenjenih fajlova na git
1. _git add -u_ -> dodavanje izmenjenih fajlova koji su izmenjeni van git-a(ako rucno obrišemo fajl ili ga premestimo)
1. _git remote add origin "link ili ssh"_ -> dodavanje izmenjenih fajlova u staged stanje pre kommita ukoliko kommitujemo na remote server
1. _git status_ -> provera statusa gita, prikaz trenutnog stanja stage-ovanih i ne stage-ovanih fajlova. Staged fajlovi su svi oni fajlovi cijeg je postojanja svestan git
1. _git commit_ -> komitovanje promena i dodavanje tog commita u history
1. _git commit -m "poruka"_ -> dodavanje poruke za commit i za commitovane fajlove, -m je flag za poruku
1. _git commit -am "poruka"_ -> koristi se ako smo stageovali sve fajlove i želimo da u jednom koraku dodamo i commitujemo. Ne može se koristiti pri prvom commitu fajla
1. _git reset HEAD ime-fajla_ -> koristi se kada zelimo da izbrišemo neki fajl sa staged stack-a, tačnije kada ne želimo da git zna išta o tom fajlu
1. _git checkout --ime-fajla_ -> koristi se kada zelimo da fajl zamenimo njegovom veryijom iy poslednjeg commit-a
1. _git log_ -> prikaz istorije commitova, poslenji je na vrhu
1. _git help log_ -> prikaz mogućih kombinacija podfunkcionalnosti help komande
1. _git log --oneline --graph --decorate --color_ -> prikaz komitova u jednoj liniji, skraceno, obojeno
1. _git rm ime-fajla_ -> brisanje commitovanog fajla
1. _git mv šta gde_ -> premestanje fajlova
1. _git push_ -> stavljanje izmena na server tako da se sve lokalne izmene na repozitorijumu primene na remote serveru
1. _git push -u_ -> kada pushujemo na remote server prvi put pushovanje izmena koje su mozda odradjene lokalno van git-a
1. _git pull_ -> povlacenje novih izmena sa remote servera tako da se sve izmene koje su na serveru primene na lokalni repozitorijum
1. _git remote set-url origin URL_ -> menjanje origina na vec postojeci git
1. _git push -u origin --all_ -> kada smo promenili origin da dodamos sve na git
1. _git rev-list --count HEAD ili branch name_ -> prebrojati broj commitova unutar jednog git repozitorijuma
1. _git shortlog -s -n_  -> ispisuje broj commitova po contributorima
1. _git branch ime_ -> pravljenje nove grane
1. _git checkout ime-grane_ -> promena grane
1. _git checkout -b ime-grane_ -> istovremeno kreiranje nove grane i prelazak na nju
1. _git merge grana-na-koju-mergujemo grana-koju-pripajamo_ - Spajanje grana
1. _git branch -d ime-grane_ - Brisanje grane


## .gitignore

U ovaj fajl stavljamo foldere i fajlove koje ne želimo da stage-ujemo. Princip funkcioniše tako da se jedan tip nalazi u jednoj liniji. Na primer: Sadržaj .gitignore fajla u kom ne želimo da se nadju folder proba i svi fajlovi sa ekstenzijom .log i sve slike sa .jpg izgledao bi ovako:

   ```git
   proba
   */.log
   */.jpg
   ```
U slučaju node_modules i novog projekta proces je sledeći

1. U gitignore kucamo:
   ```js
      'node_modules/' is added in this '.gitignore'
   ```
2. U terminalu kucamo
   
   ```bash
      git rm -r --cached node_modules
      git commit -m 'Remove the now ignored directory node_modules'
      git push origin master
   ```


## Dodavanje SSH

SSH key služi da autorizujemo uređaj da koristi remote repozitorijum bez autorizacije koprisnika svaki put kada se vrše komande za git. SSH ključ lokalno dodajemo na sledeći nacin:

   ```git
    cd ~ //navigacija na root folder
    napravimo ssh folder ako ne postoji
    cd ssh
    ssh-keygen -t rsa -C "email"
    Unosi se fajl u kom želimo da čuvamo ssh
   ```

Zatim se taj key doda i na klijentu (hosting provajderu) i vrši se verifikacija SSH:

   ```git
    ssh -T git@github.com
   ```

## Remote push na repozitorijum

Kada želimo da naš lokalni folder pushujemo na remote hosting provajder koristimo sledeći redosled komandi:

   ```git
    git remote add origin "link iz github-a"
    git commit -am "poruka"
    git push -u origin master
   ```

## Git za testing

Nakon sto je instaliran git na računar kroz Git Bash kloniramo fajl u direktorijum koji nam odgovara --> **c/xampp/htdocs** i nakon toga imamo fajl u htdocs folderu. Sve sto treba da se uradi jeste da se promeni direktorijum iz htdocs u taj folder _cd folder_ i da se pozove pri svakoj izmeni programera komanda _git pull_.Proces bi izgledao ovako:

   ```git
    instalacija gita
    pokretanje GitBash
    navigacija na htdocs
    cd putanja-do-htdocs
    git clone "url"
    promena foldera u folder u kom je projekat
    cd ime-foldera
    git pull
   ```
