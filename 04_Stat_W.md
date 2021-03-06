---
layout: page
title: 04 -- A jednak statystyka ?
mathjax: true
---


# Analiza danych

## GIGO (ang. _Garbage In, Garbage Out_)

> Wyniki przetwarzania błędnych danych zawsze będą błędne niezależnie od poprawności procedury ich przetwarzania.

Algorytmy eksploracyjne są bardzo czułe na błędne dane źródłowe. Ponieważ nie istnieje uniwersalne narzędzie do wykrywania błędnych danych, właściwe przygotowanie danych jest warunkiem koniecznym powodzenia całego projektu. 

Zawsze na początku:

1. Oceń przydatność danych w rozwiązaniu postawionego problemu (tutaj jeszcze nie modyfikuj danych)
    - jakie informacje masz w danych ?
    - Czy dane opisujące zależności między zmiennymi objaśniającymi a objaśninymi są kompletne ?
    - Czy te informacje pozwolą uzyskać odpowiedź na postawione pytanie ?
    - Jakich problemów możesz się spodziewać podczas tworzenia modeli ?

2. Wykrte w danych błędy muszą zostać usunięte tak by dopasować ich jakość do technicznych wymogów używanych modeli.

3. Dostosowanie danych do postawionego problemu - wprowadzenie do danych nowych informacji.

## Dane zawsze są błędne

Pomiar oznacza zazwyczaj dysponowanie jakimś urządzeniem pomiarowym. Narzędziem tym może być np. waga (pomiar ciężaru) jak i ankieta (pomiar stopnia zadowolenia studentów z wykładowców). Błędy pomiaru mogą być generowane przez: ograniczoną dokładność przyrządu, złe wykalibrowanie, niewłaściwa skala itp.

Ogólnie wyróżnia się dwa rodzaje błędów pomiaru:

1. _Błąd systematyczny_ (ang. _Bias_) - zawyża bądź zaniża wszystkie otrzymane wyniki. Mały wpływ na Algorytmy eksploracyjne.

2. _Błąd przypadkowy_ (ang. _Noise_) - przypadkowe zmiany otrzymywanych wyników. Duży wpływ na Algorytmy eksploracyjne. Mogą prowadzić do błędnych wniosków i znalezionych zależności.

## Jaką postać danych potrzebujemy

Aby algorytmy eksploracyjne mogły przetworzyć dane musisz sprowadzić je do postaci tabelarycznej. Kolumny takiej tabeli przedstawiają cechy analizowanych obiektów. Nazywane są często atrybutami bądź zmiennymi. Np . kolumna _Income_ zawiera informacje o zarobkach.

Zbiór atrybutów jednego obiektu nazywamy **przypadkiem**. Np. zmierzony w danym czasie zbiór wartości wszystkich atrybutów klienta.

Przykładowe dane w postaci tabelarycznej:

![TablicaDanych](img/rys4.png)

# Podział atrybutów, typy danych

Ze względu na rodzaj mierzonej wielkości atrybuty dzielimy najczęściej na **ciągłe** lub **dyskretne**. Lepszym podziałem danych jest pogrupowanie ich w następujące typy danych:

![TypyDanych](img/rys5.png)

1. **Cechy jakościowe** (_niemierzalne_, _kategoryjne_) to takie, których nie można jednoznacznie scharakteryzować za pomocą lich (czyli mie da się ich zmierzyć). Np. płeć, etykiety, kategorie produktów,grupa krwi, kolor itp.

![jakosc](img/rys6.png)

- Nie można policzyć wartości średniej, min, max.
- Nie można uporządkować wartośći.

2. **Cechy porządkowe**  umożliwiają porządkowanie wszystkich elementów zbioru wyników. Cechy takie najlepiej określa się przymiotnikami i ich stopniowaniem. Np. wzrost (niski, średni, wysoki), wykształcenie (podstawowe, średnie, wyższe), ocena filmu itp.

3. **Cechy ilościowe** (_mierzalne_) dadzą się wyrazić za pomocą jednostek miary w pewnej skali. Np. Wzrost (w cm), waga (w kg), wiek (w latach) itp.

![Ilosc](img/rys7.png)

- Można z nich policzyć wartość średniej, min, max.
- Można uporządkować wartości.

## Ważne

> Wynikiem oceny atrybutów powinno być uzyskanie odpowiedzi na następujące pytania:

1. Czy zakres wartości atrybutów obejmuje wszystkie przypadki będące przedmiotem analizy?
2. Czy częstotliwości występowania poszczególnych wartości atrybutów są zgodne z doświadczeniem i intuicją eksperta dziedzinowego?

# Wstępna analiza atrybutów

## Atrybuty jednowartościowe

Atrybuty jednowartościowe to inaczej stałe. Mamy z nimi do czynienia gdy w całej kolumnie występuje tylko jedna wartość. Ze względu, iż nie istnieją żadne zależności pomiędzy stałymi atrybutami a pozostałymi kolumnami obiektów, nie powinniśmy używać taki atrybutów do modelowania.
> Zadanie. Napisz funkcję która pobiera ramkę danych i wyrzuca wszystkie jednowartościowe kolumny.

## Atrybuty wielowartościowe (ilościowe)

Atrybut przyjmujący przynajmniej dwie wartości oznaczać będziemy jako zmienną.
>Dla zmiennej dyskretnej w pierwszej kolejności powinniśmy odnotować liczebność i częstotliwość występowania każdej z klas.
>Zmienne ciągłe powinniśmy opisywać poprzez jej podstawowe statystyki _średnią_, _odchylenie standardowe_ oraz wartość _minimalną_ i _maksymalną_.

Otrzymane rozkłady powinny zostać przeanalizowane (dyskusja z ekspertem dziedzinowym) czy nie zawierają błędów. Często nietypowy rozkład świadczy o niereprezentatywności próbki danych.

## Atrybuty różnowartościowe (jakościowe)

Atrybuty (dyskretne) posiadające wartości niepowtarzalne (np. Pesel, Email) **nie** powinny być bezpośrenio brane do procesu eksploracji danych. Po pierwsze wydłuża się czas analizy i przetwarzania takiej zmiennej. Po drugie skoro wartości nie powtarzają się, oznacza to, że nie istnieją żadne ukryte zależności między wybranym atrybutem a innymi cechami. Jeśli koniecznie chcemy tego typu atrybuty włączyć do analiz wpierw powinniśmy je pogrupować.

## Atrybuty porządkowe (monotoniczne)

Atrybuty monotoniczne to takie które stale się zwiększają lub zmniejszają. Np. Atrybuty powiązane z czasem, nr faktur, Pesel.
Nie istnieją proste metody statystyczne pozwalające wykryć atrybuty monotoniczne dlatego najlepiej przedyskutować problem z ekspertem dziedzinowym. Atrybuty te wymagają przekształcenia zanim użyjesz ich do analiz w innym przypadku często otrzymasz niereprezentatywność danego atrybutu.

## Rozkłady wartości

Poznanie dokładnych typów rozkładów wszystkich zmiennych jest bardzo istotna dla analizy danych. Inaczej nie będziemy w stanie:

1. Ocenić reprezentatywności danych (jak sprawdzić czy danych nie jest za mało ?)
2. Wykryć błędy pomiarów
3. Właściwie skonfigurować algorytm eksploracji danych.

## Integralność danych

W teorii bazy danych i hurtownie danych powinny gwarantować integralość i poprawność przechowywanych w nich danych. Rzeczywistość okazuje się jednak zupełnie inna - dane zawierają pełno błędnów. Sprawdzenie integralności powinno dać informacje o tym jak błędne dane trafiły do bazy i czy dane mogą być poprawione czy powinny być usunięte.

## Duplikaty

Jeśli dane pochodzą z wielu źródeł mogą zawierać duplikaty. Dane te zmieniają wartości rozkładów. Zawsze należy je wykryć i usunąć.

## Zakres wartości

Jest to najczęstsza metoda wykrywania błędów. Ilu klientów przeżyło więcej niż 100 lat ? ile razy wzrost zamiast w cm podany był w metrach ? Dlaczego istnieją produkty, które zostały wycofane jeszcze przed ich wprowadzeniem na rynek. Zawsze uzgodnij zakres zmiennych z ekspertem dziedzinowym.

## Wartości domyślne

Bardzo dużo błędów w danych pochodzi z wartości domyślnych, które zazwyczaj automatycznie wprowadzane są przez system. Np. domyślna data 1900-01-01.

## Weryfikacja odpowiedniej ilości danych

> Ile to jest odpowiednia ilość ? ( $>30$ ;) )
Obecnie brak uniwersalnych metod, które określiły by czy ilość posiadanych danych jest wystarczająca dla danego algorytmu.

Wymagana ilość danych zależy od:

1. Modelowanego problemu
2. Oczekiwany poziom wiarygodności wyników
3. Liczba atrybutów (im więcej cech tym więcej potrzeba danych)
4. Rozkłady atrbutów (im większe zróżnicowanie tym więcej danych)
5. Im bardziej skomplikowane zależności między przypadkami tym więcej danych potrzebujemy.

## Populacja

Populacja (całość) statystyczna zazwyczaj nie jest dostępna bo:

1. Istnieją populacje nieskończone (np. czas)
2. Zebranie danych od całej populacji jest trudne, czasochłonne i kosztowne.
3. Wykorzystanie dużej (miliony rekordów) ilości danych do eksploracji jest bardzo utrudnione ze względu na czasochłonność.

## Badanie zbieżności do rzeczywistych rozkładów

Dla zmiennej ciągłej wyrysuj histogramy dla różnej ilości przypadków np. zaczynasz od 100 a potem dodajesz kolejne 100 itd. Obeserwacja kiedy dodanie nowych danych nie zmienia (za bardzo) otrzymanego histogramu mówi ile danych jest potrzebnych.

Można również badać jak zmienia się **odchylenie standardowe** dla różnej liczebności próby. Wyniki łatwo interpretować graficznie. Odchylenie liczymy jako różnica wartości i jej średniej. Ze wzlgędu, iż różnice te mogą mieć różny znak (dodatnie, ujemne - ale $\sum_i x_i-\vec{x} = 0$) lepiej wziąć kwadrat różnicy. Wymiar tej wielkości (**Wariancja**) jest jednak niezgodny z wymiarem samej zmiennej, dlatego obliczamy pierwiastek z otrzymanej wielkości (**Odchylenie standardowe**).

W przypadku zmiennych kategoryjnych nie można policzyć średniej i odchylenia. Można za to policzyć częstości występowania w zależności od zwiększającej się ilości przypadków.

# Metody wykrywania danych oddalonych

Za wartości typowe będziemy uważać wartości określone na przedziale $\vec{x} \pm k \ast \sigma$, gdzie $\vec{x}$ oznacza wartość średnią a $\sigma$ to odchylenie standardowe. $k=2 lub 3$. Dla $k=1$ mamy pokrycie 68%, dla $k=2$ już 95%, natomiast dla 3 pokrywamy 99,7% danych.

Inną metodą określania outlierów jest **rozstęp międzykwartylowy IQR** (_ang. interquartile range_).

Kwartyle dzielą zbiór danych na 4 części, przy czym każda zawiera 25% danych. Metoda ta jest bardziej odporna niż powyższa bazująca na odchyleniu standardowym.

$IQR = Q3 - Q1$

Przedział wyznaczamy jako:
$< Q1- 1.5 \times IQR, Q3 + 1.5 \times IQR >$. [John Tukey](https://en.wikipedia.org/wiki/Box_plot)

Wartości spoza określonego przedziału uznajemy za odstające.

Graficznie wartości odstające można wyznaczyć na podstawie histogramu oraz scater plotów.

# Metody na braki danych

1. Pierwsze co można zrobić ? Pomijanie danych. Bardzon niebezpieczny krok.
2. Imputacja danych, czyli:
    - zastępowanie ich pewną stałą (0 dla numerycznych, missing dla tekstowych)
    - zastępowanie ich wartością średnią (liczbowe) bądź medianą (liczbowe, kategoryjne)
    - zastępowanie wartością losową

Wybór metody w dużej mierze zależy od typu danych.

Można również zastosować np. metodę 'k-NN' (najbliższy sąsiad) do uzupełnienia braków. Polega ona na znalezieniu k takich przykładów, które są najbardziej podobne dla uzupełnianego obiektu. Brakującą wartość wyznaczamy jako średnią z tych $k$ najbliższych wybranych wartości. W metodzie tej nie wiadomo jakie $k$ przyjąć.

# Przekształcenia danych

Dane można normalizować w celu ujednolicenia wpływu każdej zmiennej na wyniki. Główne metody normalizacji to:

1. Min-Max: liniowa transformacja pierwotnych danych najczęściej do przedziału [0,1] zgodnie ze wzorem $x' = \frac{x-min(x)}{max(x)-min(x)}$
2. Standaryzacja Z-score: Pochodzi od własności, zgodnie z którą po normalizacji wartość średnia powinna wynosić $0$. $x' = \frac{x-\vec{x}}{\sigma}$.

# Eksploracyjna analiza danych

EDA jest jedną z podstawowych technik eksploracji. Dzięki wizualizacji danych, pozwala na sprawdzenie wzeja=emnych relacji między atyrbutami i identyfikacje ciekawych podzbiorów obserwacji.

# Podstawowe pojęcia statystyczne

**Statystyka** zajmuje się zbieraniem i przetwarzaniemi informacji. To nauka poświęcona metodom badania zjawisk masowych, polega na systematyzowaniu obserwowarnych cech ilościowych i jakościowych oraz na przedstawieniu wyników w postaci table czy wykresów. Posługuje się do tego matematycznym formalizmem rachunku prawdopodobieństwa.

**Statystyka matematyczna** zajmuje się badaniem zbiorów na podstawie znajomości własności ich części.

1. **Populacja** to zbióro obiektów z wyróżnioną cechą (cechami).
2. **Próba** to wybrana część populacji podlegająca pełnemu badaniu. Wnioski z próby przenosimy na populację.
3. **Cecha** czyli wielkość losowa charatketryzująca obiekt danej populacji.
4. **Zmienna losowa** wielkość o wartośćiach rzeczywistych, określona na zbiorze zdarzeń elementarnych
5. **Dystrybuanta** opisuje rozkład kategoryjnej zmiennej losowej.
6. **Rozkład zmiennej losowej** zbiór wartości zmiennej losowej oraz prawdopodobieństwa z jakimi są przyjmowane.
7. **Wartość oczekiwana** (Liczba - średnia) $E(X)$ zmiennej losowej.
8. **Wariancja** (Liczba) charakteryzuje rozrzut zbioru wokół wartości średniej. $D(X)$
9. **Odchylenie standardowe** $D(X) = \sqrt{D(X)}$

# Metody statystyczne opisu danych

- Opisowe statystyki: średnia, mediana, min, max, dominanta (moda), odchylenie standardowe, wariancja, kurtoza itp.
- Graficzne metody: box plot, histogram, scatter plots.

## O czym mówi średnia

- ile zarabiają dyrektorzy w działach sprzedaży ?
- średnia zarobków dyrektorów sprzedaży wynosi 12161 PLN.
- Czy można określić ile zarabia konkretny dyrektor ?
- Czy dyrektorzy to bogaci ludzie ?
- Czy można obliczyć średnią płeć dyrektorów

## O czym mówi mediana

- Czy większość dyrektorów to bogaci ludzie ?
- W jakim przedziale mieszczą się zarobki większośći dyrektorów.
- Ile zarabia przeciętny dyrektor (moda) ?
- jakie zarobiki są najczęstsze

## Kwartet Anscombre'a - wizualizacja danych

**Francis Anscombe** - angielski statystyk. Studiował w Yale i Princeton.
Pionier analizy wizualnej - podkreślał istotność wizualizacji danych.
Stworzył tzw kwartet Anscombe’a.

![Ilosckwartet](img/rys8.png)

### Zadanie

>Znajdź dane i oblicz podstawowe statystyki

## Graficzna analiza danych

### Histogram

**Histogram** to graficzny sposób przedstawienia rozkładu empirycznego cechy.
Złożony z szeregu prostokątów umieszczonych na osi współrzędnych Na osi ”x” mamy przedziały klasowe wartości cechy a na osi ”y” liczebność tych przedziałów.

- Porządkuje wiedzę o analizowanych danych.
- Pokazuje odchylenia danych.
- Pokazuje dominujące dane w zbiorze.
- Używany dla danych jakościowych.

Najpopularniejsza statystyka graficzna. Domyślnie w funkcjih ist liczba 'kubełków' (ang._bins_) dobierana jest w zależności od ilości obserwacji jak i ich zmienności.

![hist](img/rys9.png)

### Scatter Plot

Jeden z najprostszych wykresów korelacyjnych między parą cech. Pomaga w diagnostyce powiązań. Wskazuje ogólny charakter i kierunek.
 
![sc1](img/rys10.png)

Rozrzuty danych.

![sc2](img/rys11.png)

### BOX PLOT

1. Wykres przedstawia medianę (środek pudełka), kwartyle (dolna i górna granica pudełka), obserwacje odstające (zaznaczone kropkami) oraz maksimum i minimum po usunięciu obserwacji odstających.
2. BoxPlot jest bardzo popularną metodą prezentacji zmienności pojedynczej zmiennej.
3. Wykres można wyznaczyć dla pojedynczej zmiennej , dla kilku zmiennych oraz dla pojedynczej zmiennej w rozbiciu na grupy.

![box](img/rys12.png)

| | BoxPlot | Histogram |
:--:|:-------:|:--------:|
Kwantyl | tak  |nie |
Mediana | tak | nie|
Wartość min |tak | tak|
Wartość max | tak |tak|
Wartość cechy | tak | tak|
Liczebność |nie|tak|
Częstość |nie |tak|
Korelacja zmiennych | nie|tak|

