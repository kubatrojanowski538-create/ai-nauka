# Rozwiazania zadan z `zadania_odczytane.pdf`

Zrodlo danych: `egzamin/zadania_odczytane.pdf`.

Kontrola spojnosci: w repozytorium nie bylo katalogu `egzamin/rozwiazania`
z dotychczasowymi odpowiedziami, wiec nie bylo czego porownac linia po linii.
Ponizsze rozwiazania zostaly policzone od nowa na danych odczytanych z PDF-a.

## Przyjete operatory i oznaczenia

- Dla systemow uogolnionych uzywam operatorow z tresci zadan:
  - implikacja Lukasiewicza: `I(a,b) = min(1, 1 - a + b)`,
  - suma ograniczona: `a op b = min(1, a + b)`,
  - iloczyn ograniczony: `a otimes b = max(0, a + b - 1)`.
- W zadaniach komputerowych zwrot "nie sa drogie" oznacza dopelnienie zbioru
  `D`, czyli `not D = 1 - D`.
- W zadaniach z sieciami boolowskimi przyjmuje wejscia boolowskie `0/1`
  i funkcje skokowa `f(n)=0` dla `n<0`, `f(n)=1` dla `n>=0`.

---

## Zdjecie 1 - grupa D

### Zadanie 1D

Mamy:

`N1=(a-x)/(2a)`, `P1=(a+x)/(2a)`,
`N2=(b-y)/(2b)`, `P2=(b+y)/(2b)`.

Poniewaz funkcje przynaleznosci sa komplementarne, suma wag regul wynosi `1`.
Wyjscie systemu:

```text
S = 4ab N1N2 - 4ab P1N2 + 4ab N1P2 + 8ab P1P2
```

Po uproszczeniu:

```text
S(x,y) = 3ab - bx + 3ay + 3xy
```

Sprawdzenie w wierzcholkach prostokata daje kolejno nastepniki regul:
`4ab`, `-4ab`, `4ab`, `8ab`.

### Zadanie 2D

Model ADALINE ma postac:

```text
y = w x + b0
```

Dla danych:

```text
(a,d1), (-a,d2), (b,d3), (-b,d4)
```

macierz rozszerzonych wejsc mozna zapisac jako:

```text
X = [ a  -a   b  -b
      1   1   1   1 ]
```

Z rownania normalnego `w* = (XX^T)^(-1) X D` dostajemy:

```text
XX^T = [ 2(a^2+b^2)   0
          0            4 ]

XD = [ a(d1-d2) + b(d3-d4)
       d1+d2+d3+d4 ]
```

Zatem:

```text
w*  = [a(d1-d2) + b(d3-d4)] / [2(a^2+b^2)]
b0* = (d1+d2+d3+d4) / 4
```

---

## Zdjecia 2 i 4 - grupa A1/B1

### Zadanie 1 - robot mobilny

Dane:

```text
z1 = max(0.9a, 0.8a) = 0.9a
z2 = max(0.2a, 0.1a) = 0.2a
z3 = max(0, 0) = 0
```

Stopnie przynaleznosci:

```text
N1=0.1, P1=0.9
N2=0.8, P2=0.2
N3=1,   P3=0
```

Niezerowe wagi regul:

```text
R1: N1 N2 N3 -> 0.1*0.8*1 = 0.08
R2: P1 N2 N3 -> 0.9*0.8*1 = 0.72
R3: N1 P2 N3 -> 0.1*0.2*1 = 0.02
R4: P1 P2 N3 -> 0.9*0.2*1 = 0.18
```

Suma wag wynosi `1`, wiec:

```text
uL = 0.08*C + 0.72*(-C) + 0.02*C + 0.18*C = -0.44 C
uR = 0.08*C + 0.72*C    + 0.02*(-C) + 0.18*C =  0.96 C
```

Odpowiedz: lewe kolo `-0.44 C`, prawe kolo `0.96 C`.

### Zadanie 2 - generator PI-TS dla 4 wejsc

Dla `zk in [-alpha_k, beta_k]`:

```text
Nk(zk) = (beta_k - zk)/(alpha_k + beta_k)
Pk(zk) = (alpha_k + zk)/(alpha_k + beta_k)
```

Generator systemu z 4 wejsciami i 16 regulami:

```text
S(z1,z2,z3,z4) =
  sum_{i1,i2,i3,i4 in {0,1}}
    m_{i1i2i3i4}(z1,z2,z3,z4) q_{i1i2i3i4}
```

gdzie:

```text
m_{i1i2i3i4} =
  A1_i1(z1) A2_i2(z2) A3_i3(z3) A4_i4(z4)
```

oraz `Ak_0 = Nk`, `Ak_1 = Pk`. Poniewaz `Nk+Pk=1`, mianownik
systemu Takagi-Sugeno jest rowny `1`.

Rownowaznie, po rozwinieciu:

```text
S(z) = g(z)^T (Omega^T)^(-1) q
```

gdzie `g(z)` zawiera jednomiany:

```text
1, z1, z2, z3, z4, z1z2, z1z3, z1z4, z2z3, z2z4, z3z4,
z1z2z3, z1z2z4, z1z3z4, z2z3z4, z1z2z3z4
```

a `Omega` jest macierza wartosci tego wektora w 16 wierzcholkach
hiperprostopadloscianu `{-alpha_k, beta_k}`.

---

## Zdjecie 3 - grupa B

### Zadanie 1B - zakup komputerow

Dane z PDF-a:

```text
N = [0.4, 0.5, 0.9]
D = [0.6, 0.4, 1.0]
S = [0.8, 0.6, 0.9]
G = [0.2, 0.4, 0.6]
A' = [0.7, 0.1, 0.2]
Q1 = [1,0], y1 = 10
Q2 = [0,1], y2 = 16
```

Antecedenty:

```text
A1 = S otimes not D = [0.2, 0.2, 0.0]
A2 = N op G       = [0.6, 0.9, 1.0]
```

Po implikacji, polaczeniu regul iloczynem ograniczonym i wnioskowaniu:

```text
B'(y1) = 0.1
B'(y2) = 0.5
```

Srodek ciezkosci:

```text
y* = (10*0.1 + 16*0.5)/(0.1+0.5) = 15
```

Odpowiedz: nalezy zakupic okolo `15` komputerow.

### Zadanie 2B - siec boolowska

Warstwa pierwsza:

```text
h1 = step(2a + b - 0.3)
h2 = step(-a - 3)
```

Dla wejsc `0/1` neuron `h2` jest zawsze rowny `0`, a `h1=1` poza
przypadkiem `a=0,b=0`. Wyjscie:

```text
f = step(5h1 - h2 - 0.2) = h1
```

Funkcja boolowska:

```text
f(a,b) = a OR b
```

---

## Zdjecia 5 i 9 - grupa F

### Zadanie 1F - GEP

Chromosom:

```text
Gen 1: OANabcaNbca
Gen 2: AOcbaabcabb
```

Drzewa ekspresji:

```text
Gen 1 = (not a AND b) OR c
Gen 2 = (c OR b) AND a
```

Polaczenie genow operatorem OR:

```text
h(a,b,c) = [(not a AND b) OR c] OR [(c OR b) AND a]
         = b OR c
```

Funkcja zadana:

```text
f(a,b,c) = (a AND not b) OR (b AND c)
```

Tabela zgodnosci daje 4 trafienia na 8 mozliwych kombinacji, wiec:

```text
accuracy = 4/8 = 0.5 = 50%
```

### Zadanie 2F - k-means

Punkty:

```text
(1,4), (2,3), (7,7), (8,6)
```

Centra poczatkowe:

```text
c1=(1,4), c2=(2,3)
```

Krok 1:

```text
C1 = {(1,4)}
C2 = {(2,3), (7,7), (8,6)}
c1 = (1,4)
c2 = ((2+7+8)/3, (3+7+6)/3) = (17/3, 16/3)
```

Krok 2:

```text
C1 = {(1,4), (2,3)}
C2 = {(7,7), (8,6)}
c1 = (1.5, 3.5)
c2 = (7.5, 6.5)
```

Krok 3 nie zmienia przydzialow, wiec wynik koncowy:

```text
C1 = {(1,4), (2,3)}, centrum (1.5, 3.5)
C2 = {(7,7), (8,6)}, centrum (7.5, 6.5)
```

---

## Zdjecia 6 i 7 - grupa E

### Zadanie 1E - kNN

Punkt testowy: `P=(4,3)`.

Kwadraty odleglosci:

```text
B (2,3), klasa o: 4
C (3,1), klasa o: 5
H (6,4), klasa *: 5
D (6,5), klasa *: 8
A (1,2), klasa o: 10
G (1,0), klasa o: 18
E (7,7), klasa *: 25
F (8,6), klasa *: 25
```

Dla `k=3` najblizsi sasiedzi to `B`, `C`, `H`, czyli dwie klasy `o`
i jedna klasa `*`.

Odpowiedz: `P` nalezy do klasy `o`.

### Zadanie 2E - PNN

Dla `sigma = 1/sqrt(2)` mamy `2 sigma^2 = 1`, wiec:

```text
K(x,xi) = exp(-||x-xi||^2)
```

Dla punktu `x=(x1,x2)`:

```text
g1(x) = 1/2 [
  exp(-((x1-1)^2  + (x2+1)^2)) +
  exp(-( x1^2     + (x2-2)^2))
]

g2(x) = 1/3 [
  exp(-((x1+3)^2 + (x2-3)^2)) +
  exp(-((x1-4)^2 + (x2-5)^2)) +
  exp(-((x1+2)^2 + (x2-2)^2))
]

g3(x) = 1/2 [
  exp(-((x1-1)^2 + x2^2)) +
  exp(-((x1-2)^2 + (x2-2)^2))
]
```

Regula decyzyjna:

```text
class(x) = arg max {g1(x), g2(x), g3(x)}
```

---

## Zdjecie 8 - grupa A, budynki i ACC = 0.7

### Zadanie 1A - remont budynku

Dane:

```text
Z = [0.5, 0.6, 0.7]
W = [0.4, 0.6, 0.3]
D = [0.2, 0.8, 0.6]
A' = [1, 0.5, 0.5]
Q1 = [1, 1, 0]
Q2 = [1, 1, 0.2]
Q3 = [1, 0.5, 0.4]
nominalnie: y1=60, y2=30, y3=20
```

Antecedent `Z AND W AND D = min(Z,W,D)`:

```text
[0.2, 0.6, 0.3]
```

Po wyznaczeniu relacji, polaczeniu regul i wnioskowaniu:

```text
B' = [1.0, 1.0, 0.8]
```

Racjonalne wyostrzenie skladowe dla liczby pracownikow na zmianach:

```text
rano      = 60 * 1.0 = 60
poludnie  = 30 * 1.0 = 30
wieczor   = 20 * 0.8 = 16
```

Odpowiedz: `60` rano, `30` w poludnie, `16` wieczorem.

### Zadanie 2A - ACC i wazona czulosc

Dane:

```text
t = [a,a,a,b,b,c,c,c,b,Y]
p = [a,c,a,b,a,c,c,b,b,c]
ACC = 0.7
```

Bez ostatniego rekordu jest 6 trafien. Do `ACC=0.7` na 10 rekordach potrzeba
7 trafien, wiec:

```text
Y = c
```

Macierz rozbieznosci, wiersze = klasa rzeczywista, kolumny = predykcja:

```text
      a  b  c
a     2  0  1
b     1  2  0
c     0  1  3
```

Czulosc klasowa:

```text
SEN_a = 2/3
SEN_b = 2/3
SEN_c = 3/4
```

Wazona czulosc:

```text
SEN_w = (3*(2/3) + 3*(2/3) + 4*(3/4))/10 = 0.7
```

---

## Zdjecie 11 - grupa B, siec 2-1-2 i TSK

### Zadanie 1B - backpropagation dla `w1,2` i `b1`

Zbior uczacy ma postac:

```text
U = { (p1^(k), p2^(k), t4^(k), t5^(k)) : k=1,...,N }
```

Dla jednego przykladu:

```text
E = 0.6 e4^2 + 0.4 e5^2
e4 = t4 - a4
e5 = t5 - a5
```

Definiujac lokalny sygnal bledu jako `delta_i = -dE/dn_i`, dostajemy:

```text
delta4 = 1.2 e4 f4'(n4)
delta5 = 0.8 e5 f5'(n5)
delta3 = f3'(n3) (w4,3 delta4 + w5,3 delta5)
delta1 = f1'(n1) w3,1 delta3
```

Aktualizacja metoda najszybszego spadku:

```text
w1,2 <- w1,2 + eta delta1 p2
b1   <- b1   + eta delta1
```

### Zadanie 2B - system TSK

Funkcja:

```text
S(x1,x2) = 1 + x1 - x2 + 5 x1 x2
```

Przedzialy:

```text
x1 in [-2,0], x2 in [0,1]
```

Funkcje przynaleznosci:

```text
N1(x1) = -x1/2
P1(x1) = (2+x1)/2

N2(x2) = 1-x2
P2(x2) = x2
```

Nastepniki regul to wartosci funkcji w wierzcholkach:

```text
qNN = S(-2,0) = -1
qPN = S(0,0)  =  1
qNP = S(-2,1) = -12
qPP = S(0,1)  =  0
```

---

## Zdjecie 12 - widoczne zadanie 2

Siec boolowska z trzema wejsciami:

```text
h1 = step(a - b + 2c + 0.5)
h2 = step(a - b + c - 0.5)
f  = step(h1 + h2 - 1.5)
```

Dla wejsc `0/1` wyjscie jest rowne `1` dla:

```text
001, 100, 101, 111
```

Funkcja:

```text
f(a,b,c) = (not b AND (a OR c)) OR (a AND b AND c)
```

Rownowaznie:

```text
f(a,b,c) = (a AND not b) OR (c AND not b) OR (a AND c)
```

---

## Zdjecie 13 - grupa B, SVM, backpropagation, metryki

### Zadanie 1 - SVM

Dane:

```text
x1=(0,0), y1=-1
x2=(0,1), y2= 1
x3=(1,0), y3= 1
x4=(1,1), y4=-1
sigma = 1/sqrt(3)
```

Dla jadra Gaussa:

```text
K(u,v)=exp(-||u-v||^2/(2 sigma^2))
```

tu `2 sigma^2 = 2/3`, wiec dla odleglosci kwadratowej `1` mamy
`r=e^(-3/2)`, a dla odleglosci kwadratowej `2` mamy `s=e^(-3)`.

Macierz jadra:

```text
K = [ 1   r   r   s
      r   1   s   r
      r   s   1   r
      s   r   r   1 ]
```

Macierz Hessego `H_ij = y_i y_j K(x_i,x_j)`:

```text
H = [ 1  -r  -r   s
     -r   1   s  -r
     -r   s   1  -r
      s  -r  -r   1 ]
```

Problem dualny mozna zapisac jako minimalizacje:

```text
min_lambda  1/2 lambda^T H lambda - 1^T lambda
```

przy ograniczeniach:

```text
sum_i lambda_i y_i = 0
lambda_i >= 0
```

czyli:

```text
-lambda1 + lambda2 + lambda3 - lambda4 = 0
lambda_i >= 0
```

Jesli formulujemy wersje z miekkim marginesem, dochodzi ograniczenie
`lambda_i <= C`.

### Zadanie 2 - backpropagation

Zbior uczacy:

```text
U = { (p1^(k), p2^(k), t4^(k), t5^(k)) : k=1,...,N }
```

Dla:

```text
E = 1/4 (t4-a4)^2 + 3/4 (t5-a5)^2
f_i'(n_i) = alpha a_i(1-a_i)
```

lokalne sygnaly bledu:

```text
delta4 = 1/2 e4 alpha a4(1-a4)
delta5 = 3/2 e5 alpha a5(1-a5)
delta3 = alpha a3(1-a3) (w4,3 delta4 + w5,3 delta5)
delta1 = alpha a1(1-a1) w3,1 delta3
```

Aktualizacja:

```text
w1,2 <- w1,2 + eta delta1 p2
```

Analogicznie dla przesuniecia neuronu 1:

```text
b1 <- b1 + eta delta1
```

### Zadanie 3 - metryki klasyfikatora binarnego

Dla klasy pozytywnej `b`:

```text
TP = 4, FN = 2, FP = 1, TN = 5
```

Metryki:

```text
ACC = (TP+TN)/12 = 9/12 = 0.75
SEN = TP/(TP+FN) = 4/6 = 2/3
SPEC = TN/(TN+FP) = 5/6
```

Gdyby za klase pozytywna przyjac `a`, czulosc i specyficznosc zamieniaja sie
miejscami.

---

## Zdjecie 14 - wariant z komputerami

Dane:

```text
N = [0.7, 0.6, 0.1]
D = [0.9, 0.7, 0.3]
S = [0.5, 0.9, 0.8]
G = [0.1, 0.6, 0.6]
A' = [0.4, 0.5, 0.8]
Q1 = [1,0], y1=10
Q2 = [0,1], y2=20
```

Antecedenty:

```text
A1 = S otimes not D = [0.0, 0.2, 0.5]
A2 = N op G       = [0.8, 1.0, 0.7]
```

Wynik wnioskowania:

```text
B'(y1) = 0.1
B'(y2) = 0.4
```

Srodek ciezkosci:

```text
y* = (10*0.1 + 20*0.4)/(0.1+0.4) = 18
```

Odpowiedz: nalezy zakupic okolo `18` komputerow.

---

## Zdjecie 15 - grupa A, budynki i ACC = 0.5

### Zadanie 1A - remont budynku

Dane:

```text
Z = [0.8, 0.9, 0.7]
W = [0.6, 0.8, 0.5]
D = [0.6, 0.8, 0.7]
A' = [1, 0.5, 0.5]
Q1 = [1, 0, 0]
Q2 = [1, 1, 0.2]
Q3 = [1, 0.5, 0.4]
nominalnie: y1=24, y2=16, y3=10
```

Antecedent `min(Z,W,D)`:

```text
[0.6, 0.8, 0.5]
```

Wynik wnioskowania:

```text
B' = [1.0, 0.3, 0.0]
```

Racjonalne wyostrzenie skladowe:

```text
rano      = 24 * 1.0 = 24
poludnie  = 16 * 0.3 = 4.8
wieczor   = 10 * 0.0 = 0
```

Odpowiedz: `24` rano, okolo `5` w poludnie, `0` wieczorem.

### Zadanie 2A - ACC i wazona czulosc

Dane:

```text
t = [a,a,b,b,b,c,c,X]
p = [a,b,b,a,a,a,c,c]
ACC = 0.5
```

Bez ostatniego rekordu sa 3 trafienia. Do `ACC=0.5` na 8 rekordach potrzeba
4 trafien, wiec:

```text
X = c
```

Macierz rozbieznosci:

```text
      a  b  c
a     1  1  0
b     2  1  0
c     1  0  2
```

Wazona czulosc:

```text
SEN_w = liczba trafien / liczba rekordow = 4/8 = 0.5
```

---

## Zdjecie 16 - grupa C

### Zadanie 1C - backpropagation dla `w3,1` i `b3`

Zbior uczacy:

```text
U = { (p1^(k), p2^(k), t4^(k), t5^(k)) : k=1,...,N }
```

Dla:

```text
E = 0.4 e4^2 + 0.6 e5^2
e4 = t4 - a4
e5 = t5 - a5
```

lokalne sygnaly bledu:

```text
delta4 = 0.8 e4 f4'(n4)
delta5 = 1.2 e5 f5'(n5)
delta3 = f3'(n3) (w4,3 delta4 + w5,3 delta5)
```

Aktualizacje:

```text
w3,1 <- w3,1 + eta delta3 p1
b3   <- b3   + eta delta3
```

### Zadanie 2C - SVM

Dane:

```text
x1=(-1,-1), y1=-1
x2=(-1, 1), y2= 1
x3=( 1,-1), y3= 1
x4=( 1, 1), y4=-1
sigma = sqrt(2)
```

Tu `2 sigma^2 = 4`, wiec dla odleglosci kwadratowej `4` mamy `r=e^(-1)`,
a dla odleglosci kwadratowej `8` mamy `s=e^(-2)`.

Macierz jadra:

```text
K = [ 1   r   r   s
      r   1   s   r
      r   s   1   r
      s   r   r   1 ]
```

Macierz Hessego:

```text
H = [ 1  -r  -r   s
     -r   1   s  -r
     -r   s   1  -r
      s  -r  -r   1 ]
```

Problem dualny:

```text
min_lambda  1/2 lambda^T H lambda - 1^T lambda

pod warunkami:
-lambda1 + lambda2 + lambda3 - lambda4 = 0
lambda_i >= 0
```

W wersji z miekkim marginesem dodatkowo `lambda_i <= C`.

---

## Zdjecie 19 - grupa A, komputery i siec boolowska

### Zadanie 1A - zakup komputerow

Dane:

```text
N = [0.9, 0.4, 0.4]
D = [1.0, 0.6, 0.1]
S = [0.7, 1.0, 0.7]
G = [1.0, 0.2, 0.3]
A' = [0.0, 0.8, 0.2]
Q1 = [1,0], y1=12
Q2 = [0,1], y2=24
```

Antecedenty:

```text
A1 = S otimes not D = [0.0, 0.4, 0.6]
A2 = N op G       = [1.0, 0.6, 0.7]
```

Wynik wnioskowania:

```text
B'(y1) = 0.2
B'(y2) = 0.4
```

Srodek ciezkosci:

```text
y* = (12*0.2 + 24*0.4)/(0.2+0.4) = 20
```

Odpowiedz: nalezy zakupic okolo `20` komputerow.

### Zadanie 2A - siec boolowska

Warstwa pierwsza:

```text
h1 = step(a - b + 0.5)
h2 = step(-a - b - 1)
```

Dla wejsc `0/1` neuron `h2` jest zawsze rowny `0`, wiec:

```text
f = step(0.5 h1 - h2 - 0.2) = h1
```

Neuron `h1` jest rowny `0` tylko dla `a=0,b=1`.

Funkcja:

```text
f(a,b) = a OR not b
```
