# new_service

![Logo usługi TeleKonsultacje](images/logo.png)

Repozytorium dokumentacji rozwoju nowej usługi medycznej **Telekonsultacje zdrowotne**,
prowadzone przy użyciu systemu kontroli wersji **Git** i platformy **GitHub**.

- **Przedmiot:** System kontroli wersji - edycja 7
- **Autor:** **Leon Petruńko** *(nowe nazwisko Wasilkowski)*
- **Numer słuchacza:** *PD5609*
- **Wersja dokumentacji:** `v1.0` – Gotowy plan wdrożenia usługi medycznej

## Spis treści

1. [Opis usługi medycznej](#opis-usługi-medycznej)
2. [Dokumenty w repozytorium](#dokumenty-w-repozytorium)
3. [Praca z repozytorium](#praca-z-repozytorium)
4. [Wykorzystane polecenia Git](#wykorzystane-polecenia-git)
5. [Tryb scalenia gałęzi marketing](#tryb-scalenia-gałęzi-marketing)
6. [Napotkane problemy i ich rozwiązania](#napotkane-problemy-i-ich-rozwiązania)

## Opis usługi medycznej

**Telekonsultacje zdrowotne** umożliwiają pacjentom uzyskanie porady medycznej bez
konieczności fizycznej wizyty w gabinecie lekarskim. Pacjenci kontaktują się z lekarzami
za pośrednictwem wideokonferencji, telefonu lub komunikatorów internetowych.

Cele usługi:

- poprawa dostępności do usług zdrowotnych,
- obniżenie kosztów leczenia.

## Dokumenty w repozytorium

| Plik / katalog | Zawartość |
| --- | --- |
| `README.md` | dokumentacja projektu (ten plik) |
| `opis_uslugi.txt` | nazwa, opis i cele usługi oraz sekcja „Korzyści dla pacjentów” |
| `plan_wdrozenia.txt` | etapy wdrożenia usługi wraz z terminami |
| `ryzyka.txt` | analiza potencjalnych ryzyk związanych z wprowadzeniem usługi |
| `kampania_marketingowa.txt` | plan kampanii promującej usługę (gałąź `marketing`) |
| `ankieta_pacjentow.txt` | pytania ankiety o oczekiwania i opinie pacjentów (gałąź `marketing`) |
| `images/logo.png` | logo usługi |
| `images/.gitkeep` | pusty plik, dzięki któremu Git śledził katalog `images`, zanim pojawiło się w nim logo |
| `.gitignore` | lista plików ignorowanych przez Git (prywatny plik `moje_notatki.txt`) |
| `.gitattributes` | ustawienie traktowania plików `.png` jako binarnych |

## Praca z repozytorium

### Pobranie repozytorium

```bash
# przez SSH (wymaga klucza SSH dodanego do konta GitHub)
git clone git@github.com:dreduno/new_service_PD5609.git

# lub przez HTTPS
git clone https://github.com/dreduno/new_service_PD5609.git

cd new_service_PD5609
```

Aktualizacja lokalnej kopii o najnowsze zmiany z GitHuba:

```bash
git pull
```

### Nawigacja po gałęziach

```bash
git branch              # lista gałęzi lokalnych (bieżąca oznaczona *)
git branch -a           # gałęzie lokalne i zdalne
git switch marketing    # przełączenie na gałąź marketing
git switch main         # powrót na gałąź główną
git switch -c nowa      # utworzenie nowej gałęzi i przełączenie się na nią
```

### Przeglądanie historii i przywracanie wcześniejszych wersji

```bash
# historia zmian
git log --oneline --graph
git log --oneline -- opis_uslugi.txt     # historia jednego pliku

# podgląd zmian w wybranym commicie
git show <hash>

# przywrócenie pliku do wersji z wybranego commitu
git restore --source <hash> opis_uslugi.txt

# odrzucenie niezatwierdzonych zmian w pliku
git restore opis_uslugi.txt

# cofnięcie zmian z commitu przez nowy commit (bez usuwania historii)
git revert <hash>

# podgląd całej dokumentacji w wersji oznaczonej tagiem v1.0
git switch --detach v1.0
git switch main          # powrót do bieżącej wersji
```

`<hash>` to identyfikator commitu widoczny w wyniku `git log --oneline` (np. `d6525d4`).

## Wykorzystane polecenia Git

| Polecenie | Zastosowanie w projekcie |
| --- | --- |
| `git init -b main` | utworzenie lokalnego repozytorium `new_service` z gałęzią główną `main` |
| `git add <plik>` | dodanie plików do indeksu (przygotowanie do commitu) |
| `git commit -m "..."` | zapisanie zmian w historii z opisem, np. „Inicjalizacja projektu” |
| `git status` | sprawdzenie stanu repozytorium, m.in. że `moje_notatki.txt` jest ignorowany |
| `.gitignore` | wykluczenie prywatnego pliku `moje_notatki.txt` ze śledzenia |
| `.gitkeep` | umożliwienie śledzenia pustego katalogu `images` |
| `.gitattributes` | oznaczenie plików `*.png` jako binarnych (`*.png binary`) |
| `git check-attr -a` | sprawdzenie, że Git traktuje `images/logo.png` jako plik binarny |
| `git switch -c marketing` | utworzenie gałęzi `marketing` i przełączenie się na nią |
| `git switch main` | powrót na gałąź główną |
| `git merge marketing` | scalenie gałęzi `marketing` z `main` |
| `git log --oneline --graph` | przegląd historii i struktury gałęzi |
| `git tag -a v1.0 -m "..."` | oznaczenie gotowej wersji dokumentacji tagiem z opisem |
| `git remote add origin <adres>` | połączenie repozytorium lokalnego ze zdalnym na GitHubie |
| `git push -u origin main` | wysłanie gałęzi `main` na GitHub i ustawienie jej śledzenia |
| `git push origin v1.0` | wysłanie tagu `v1.0` na GitHub |

## Tryb scalenia gałęzi marketing

Po wykonaniu `git merge marketing` Git wyświetlił komunikat:

```text
Updating b6ce8f9..fb53396
Fast-forward
 ankieta_pacjentow.txt     | 4 ++++
 kampania_marketingowa.txt | 4 ++++
```

Gałąź `marketing` została więc scalona w trybie **fast-forward** (przewinięcie do przodu).

**Dlaczego Git wybrał ten tryb?** Od momentu utworzenia gałęzi `marketing` na gałęzi `main`
nie powstał żaden nowy commit. Gałąź `main` była więc bezpośrednim przodkiem gałęzi
`marketing`. Git nie musiał niczego łączyć, wystarczyło przesunąć wskaźnik `main`
na ostatni commit gałęzi `marketing`. Nie powstał przy tym osobny commit scalający,
a historia pozostała liniowa:

```text
* fb53396 Dodano ankietę dla pacjentów
* e959924 Dodano plan kampanii marketingowej
* b6ce8f9 Dodano analizę ryzyk dla usługi
* ...
```

**Różnica w porównaniu ze scalaniem z zadania GIT_7.** W zadaniu GIT_7 obie gałęzie (`main`
i `test`) miały po rozgałęzieniu własne, nowe commity, więc ich historie się rozeszły.
Przesunięcie wskaźnika nie było wtedy możliwe. Git wykonał scalenie trójstronne
(strategia `ort`), które porównuje obie gałęzie z ich wspólnym przodkiem i tworzy nowy
**commit scalający (merge commit)** z dwoma rodzicami. Ponieważ obie gałęzie zmieniły to samo
miejsce w pliku `README.md`, wystąpił konflikt, który trzeba było rozwiązać ręcznie.
W historii widać wtedy rozgałęzienie i połączenie:

```text
*   Scalenie gałęzi test
|\
| * zmiana na gałęzi test
* | zmiana na gałęzi main
|/
* wspólny przodek
```

| Cecha | Fast-forward (`marketing`) | Scalenie trójstronne (GIT_7) |
| --- | --- | --- |
| Nowe commity na `main` po rozgałęzieniu | brak | były |
| Commit scalający | nie powstaje | powstaje (dwa rodzice) |
| Historia | liniowa | rozgałęziona |
| Możliwość konfliktu | nie | tak |

## Napotkane problemy i ich rozwiązania

| Problem | Rozwiązanie |
| --- | --- |
| `git push` przez HTTPS zwracał błąd `Password authentication is not supported` | GitHub nie przyjmuje hasła do konta w terminalu. Skonfigurowałem klucz SSH (`ssh-keygen -t ed25519`), dodałem klucz publiczny w ustawieniach konta GitHub i zmieniłem adres zdalnego repozytorium na SSH (`git remote set-url origin git@github.com:...`). |
| Gałąź główna nazywała się `master` zamiast `main` | Zmieniłem nazwę gałęzi poleceniem `git branch -m master main`, a w nowym repozytorium użyłem `git init -b main`. |
| `git pull` zwracał błąd `invalid value for 'pull.rebase': 'false.'` | W konfiguracji zapisała się wartość z kropką. Usunąłem błędny wpis (`git config --global --unset pull.rebase`) i ustawiłem poprawną wartość `git config --global pull.rebase false`. |
| Nie można było przełączyć gałęzi z powodu niedokończonego `git rebase -i` | Dokończyłem operację poleceniem `git rebase --continue` (alternatywnie można ją przerwać przez `git rebase --abort`). |
