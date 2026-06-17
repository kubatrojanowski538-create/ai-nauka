# Rozwiazania zadan z `zadania_odczytane.pdf`

Zrodlo danych: `egzamin/zadania_odczytane.pdf`.

Kontrola spojnosci: w repozytorium nie bylo katalogu `egzamin/rozwiazania`
z dotychczasowymi odpowiedziami, wiec nie bylo czego porownac linia po linii.
Ponizsze rozwiazania zostaly policzone od nowa na danych odczytanych z PDF-a.

## Przyjete operatory i oznaczenia

Dla systemow uogolnionych uzywam operatorow z tresci zadan:

$$
\begin{aligned}
I(a,b) &= \min(1, 1-a+b) && \text{implikacja Lukasiewicza},\\
a \oplus b &= \min(1, a+b) && \text{suma ograniczona},\\
a \otimes b &= \max(0, a+b-1) && \text{iloczyn ograniczony}.
\end{aligned}
$$

W zadaniach komputerowych zwrot "nie sa drogie" oznacza dopelnienie zbioru
$D$, czyli $\neg D = 1-D$. W zadaniach z sieciami boolowskimi przyjmuje wejscia
boolowskie $0/1$ oraz funkcje skokowa:

$$
f(n)=
\begin{cases}
0, & n<0,\\
1, & n\ge 0.
\end{cases}
$$

---

## Zdjecie 1 - grupa D

### Zadanie 1D

Funkcje przynaleznosci:

$$
\begin{aligned}
N_1(x) &= \frac{a-x}{2a}, & P_1(x) &= \frac{a+x}{2a},\\
N_2(y) &= \frac{b-y}{2b}, & P_2(y) &= \frac{b+y}{2b}.
\end{aligned}
$$

Poniewaz funkcje przynaleznosci sa komplementarne, suma wag regul wynosi $1$.
Wyjscie systemu:

$$
\begin{aligned}
S &= 4ab\,N_1N_2 - 4ab\,P_1N_2 + 4ab\,N_1P_2 + 8ab\,P_1P_2\\
  &= 3ab - bx + 3ay + 3xy.
\end{aligned}
$$

Sprawdzenie w wierzcholkach prostokata daje kolejno nastepniki regul:
$4ab$, $-4ab$, $4ab$, $8ab$.

### Zadanie 2D

Model ADALINE:

$$
y = wx + b_0.
$$

Dla danych $(a,d_1)$, $(-a,d_2)$, $(b,d_3)$, $(-b,d_4)$ macierz rozszerzonych
wejsc zapisujemy jako:

$$
X =
\begin{bmatrix}
a & -a & b & -b\\
1 & 1 & 1 & 1
\end{bmatrix},
\qquad
D=\begin{bmatrix}d_1\\d_2\\d_3\\d_4\end{bmatrix}.
$$

Z rownania normalnego $w^*=(XX^T)^{-1}XD$:

$$
XX^T =
\begin{bmatrix}
2(a^2+b^2) & 0\\
0 & 4
\end{bmatrix},
\qquad
XD =
\begin{bmatrix}
a(d_1-d_2)+b(d_3-d_4)\\
d_1+d_2+d_3+d_4
\end{bmatrix}.
$$

Zatem:

$$
\boxed{
\begin{aligned}
w^* &= \frac{a(d_1-d_2)+b(d_3-d_4)}{2(a^2+b^2)},\\
b_0^* &= \frac{d_1+d_2+d_3+d_4}{4}.
\end{aligned}}
$$

---

## Zdjecia 2 i 4 - grupa A1/B1

### Zadanie 1 - robot mobilny

Dane wejsciowe daja:

$$
\begin{aligned}
z_1 &= \max(0.9a,0.8a)=0.9a,\\
z_2 &= \max(0.2a,0.1a)=0.2a,\\
z_3 &= \max(0,0)=0.
\end{aligned}
$$

Stopnie przynaleznosci:

$$
N_1=0.1,\quad P_1=0.9,\qquad
N_2=0.8,\quad P_2=0.2,\qquad
N_3=1,\quad P_3=0.
$$

Niezerowe wagi regul:

| Regula | Waga |
|---|---:|
| $R_1:N_1N_2N_3$ | $0.1\cdot0.8\cdot1=0.08$ |
| $R_2:P_1N_2N_3$ | $0.9\cdot0.8\cdot1=0.72$ |
| $R_3:N_1P_2N_3$ | $0.1\cdot0.2\cdot1=0.02$ |
| $R_4:P_1P_2N_3$ | $0.9\cdot0.2\cdot1=0.18$ |

Suma wag wynosi $1$, wiec:

$$
\begin{aligned}
u_L &= 0.08C + 0.72(-C) + 0.02C + 0.18C = -0.44C,\\
u_R &= 0.08C + 0.72C + 0.02(-C) + 0.18C = 0.96C.
\end{aligned}
$$

Odpowiedz: lewe kolo $-0.44C$, prawe kolo $0.96C$.

### Zadanie 2 - generator PI-TS dla 4 wejsc

Dla $z_k\in[-\alpha_k,\beta_k]$:

$$
N_k(z_k)=\frac{\beta_k-z_k}{\alpha_k+\beta_k},
\qquad
P_k(z_k)=\frac{\alpha_k+z_k}{\alpha_k+\beta_k}.
$$

Generator systemu z 4 wejsciami i 16 regulami:

$$
S(z_1,z_2,z_3,z_4)=
\sum_{i_1,i_2,i_3,i_4\in\{0,1\}}
  m_{i_1i_2i_3i_4}(z_1,z_2,z_3,z_4)\,q_{i_1i_2i_3i_4},
$$

$$
m_{i_1i_2i_3i_4}=A_{1,i_1}(z_1)A_{2,i_2}(z_2)A_{3,i_3}(z_3)A_{4,i_4}(z_4),
$$

gdzie $A_{k,0}=N_k$ oraz $A_{k,1}=P_k$. Poniewaz $N_k+P_k=1$, mianownik
systemu Takagi-Sugeno jest rowny $1$.

Rownowaznie, po rozwinieciu:

$$
S(z)=g(z)^T(\Omega^T)^{-1}q,
$$

gdzie:

$$
\begin{aligned}
g(z)=(&1,z_1,z_2,z_3,z_4,z_1z_2,z_1z_3,z_1z_4,z_2z_3,z_2z_4,z_3z_4,\\
&z_1z_2z_3,z_1z_2z_4,z_1z_3z_4,z_2z_3z_4,z_1z_2z_3z_4)^T.
\end{aligned}
$$

Macierz $\Omega$ zawiera wartosci tego wektora w 16 wierzcholkach
hiperprostopadloscianu $\{-\alpha_k,\beta_k\}$.

---

## Zdjecie 3 - grupa B

### Zadanie 1B - zakup komputerow

Dane z PDF-a:

$$
\begin{aligned}
N&=[0.4,0.5,0.9], & D&=[0.6,0.4,1.0],\\
S&=[0.8,0.6,0.9], & G&=[0.2,0.4,0.6],\\
A'&=[0.7,0.1,0.2], & Q_1&=[1,0],\; Q_2=[0,1],\\
y_1&=10, & y_2&=16.
\end{aligned}
$$

Antecedenty:

$$
\begin{aligned}
A_1 &= S\otimes \neg D = [0.2,0.2,0.0],\\
A_2 &= N\oplus G = [0.6,0.9,1.0].
\end{aligned}
$$

Po implikacji, polaczeniu regul iloczynem ograniczonym i wnioskowaniu:

$$
B'(y_1)=0.1,
\qquad
B'(y_2)=0.5.
$$

Srodek ciezkosci:

$$
y^*=\frac{10\cdot0.1+16\cdot0.5}{0.1+0.5}=15.
$$

Odpowiedz: nalezy zakupic okolo $15$ komputerow.

### Zadanie 2B - siec boolowska

Warstwa pierwsza:

$$
h_1=\operatorname{step}(2a+b-0.3),
\qquad
h_2=\operatorname{step}(-a-3).
$$

Dla wejsc $0/1$ neuron $h_2$ jest zawsze rowny $0$, a $h_1=1$ poza
przypadkiem $a=0,b=0$. Wyjscie:

$$
f=\operatorname{step}(5h_1-h_2-0.2)=h_1.
$$

Funkcja boolowska:

$$
\boxed{f(a,b)=a\lor b}.
$$

---

## Zdjecia 5 i 9 - grupa F

### Zadanie 1F - GEP

Chromosom:

```text
Gen 1: OANabcaNbca
Gen 2: AOcbaabcabb
```

Drzewa ekspresji:

$$
\begin{aligned}
\text{Gen 1} &= (\neg a\land b)\lor c,\\
\text{Gen 2} &= (c\lor b)\land a.
\end{aligned}
$$

Polaczenie genow operatorem OR:

$$
\begin{aligned}
h(a,b,c) &= [((\neg a\land b)\lor c)]\lor[((c\lor b)\land a)]\\
         &= b\lor c.
\end{aligned}
$$

Funkcja zadana:

$$
f(a,b,c)=(a\land\neg b)\lor(b\land c).
$$

Tabela zgodnosci daje 4 trafienia na 8 mozliwych kombinacji, wiec:

$$
\operatorname{accuracy}=\frac{4}{8}=0.5=50\%.
$$

### Zadanie 2F - k-means

Punkty:

$$
(1,4),\;(2,3),\;(7,7),\;(8,6),
\qquad
c_1^{(0)}=(1,4),\;c_2^{(0)}=(2,3).
$$

Krok 1:

$$
\begin{aligned}
C_1^{(1)}&=\{(1,4)\},\\
C_2^{(1)}&=\{(2,3),(7,7),(8,6)\},\\
c_1^{(1)}&=(1,4),\\
c_2^{(1)}&=\left(\frac{2+7+8}{3},\frac{3+7+6}{3}\right)=\left(\frac{17}{3},\frac{16}{3}\right).
\end{aligned}
$$

Krok 2:

$$
\begin{aligned}
C_1^{(2)}&=\{(1,4),(2,3)\}, & c_1^{(2)}&=(1.5,3.5),\\
C_2^{(2)}&=\{(7,7),(8,6)\}, & c_2^{(2)}&=(7.5,6.5).
\end{aligned}
$$

Krok 3 nie zmienia przydzialow, wiec wynik koncowy:

$$
\boxed{
C_1=\{(1,4),(2,3)\},\; c_1=(1.5,3.5),
\qquad
C_2=\{(7,7),(8,6)\},\; c_2=(7.5,6.5)
}.
$$

---

## Zdjecia 6 i 7 - grupa E

### Zadanie 1E - kNN

Punkt testowy: $P=(4,3)$.

| Punkt | Klasa | $d^2(P,\cdot)$ |
|---|:---:|---:|
| $B=(2,3)$ | $o$ | 4 |
| $C=(3,1)$ | $o$ | 5 |
| $H=(6,4)$ | $*$ | 5 |
| $D=(6,5)$ | $*$ | 8 |
| $A=(1,2)$ | $o$ | 10 |
| $G=(1,0)$ | $o$ | 18 |
| $E=(7,7)$ | $*$ | 25 |
| $F=(8,6)$ | $*$ | 25 |

Dla $k=3$ najblizsi sasiedzi to $B$, $C$, $H$, czyli dwie klasy $o$ i jedna
klasa $*$.

Odpowiedz: $P$ nalezy do klasy $o$.

### Zadanie 2E - PNN

Dla $\sigma=1/\sqrt{2}$ mamy $2\sigma^2=1$, wiec:

$$
K(x,x_i)=\exp(-\lVert x-x_i\rVert^2).
$$

Dla punktu $x=(x_1,x_2)$:

$$
\begin{aligned}
g_1(x)&=\frac12\left[
\exp(-((x_1-1)^2+(x_2+1)^2))+
\exp(-(x_1^2+(x_2-2)^2))
\right],\\
g_2(x)&=\frac13\left[
\exp(-((x_1+3)^2+(x_2-3)^2))+
\exp(-((x_1-4)^2+(x_2-5)^2))+
\exp(-((x_1+2)^2+(x_2-2)^2))
\right],\\
g_3(x)&=\frac12\left[
\exp(-((x_1-1)^2+x_2^2))+
\exp(-((x_1-2)^2+(x_2-2)^2))
\right].
\end{aligned}
$$

Regula decyzyjna:

$$
\operatorname{class}(x)=\arg\max_{k\in\{1,2,3\}} g_k(x).
$$

---

## Zdjecie 8 - grupa A, budynki i ACC = 0.7

### Zadanie 1A - remont budynku

Dane:

$$
\begin{aligned}
Z&=[0.5,0.6,0.7], & W&=[0.4,0.6,0.3], & D&=[0.2,0.8,0.6],\\
A'&=[1,0.5,0.5], & Q_1&=[1,1,0], & Q_2&=[1,1,0.2],\\
Q_3&=[1,0.5,0.4], & y_1&=60, & y_2&=30,\; y_3=20.
\end{aligned}
$$

Antecedent:

$$
Z\land W\land D=\min(Z,W,D)=[0.2,0.6,0.3].
$$

Po wyznaczeniu relacji, polaczeniu regul i wnioskowaniu:

$$
B'=[1.0,1.0,0.8].
$$

Racjonalne wyostrzenie skladowe dla liczby pracownikow na zmianach:

$$
\begin{aligned}
\text{rano} &= 60\cdot1.0=60,\\
\text{poludnie} &= 30\cdot1.0=30,\\
\text{wieczor} &= 20\cdot0.8=16.
\end{aligned}
$$

Odpowiedz: $60$ rano, $30$ w poludnie, $16$ wieczorem.

### Zadanie 2A - ACC i wazona czulosc

Dane:

$$
t=[a,a,a,b,b,c,c,c,b,Y],
\qquad
p=[a,c,a,b,a,c,c,b,b,c],
\qquad
\operatorname{ACC}=0.7.
$$

Bez ostatniego rekordu jest 6 trafien. Do $\operatorname{ACC}=0.7$ na 10
rekordach potrzeba 7 trafien, wiec:

$$
Y=c.
$$

Macierz rozbieznosci, wiersze = klasa rzeczywista, kolumny = predykcja:

$$
CM=
\begin{array}{c|ccc}
 & a & b & c\\ \hline
a & 2 & 0 & 1\\
b & 1 & 2 & 0\\
c & 0 & 1 & 3
\end{array}
$$

Czulosc klasowa:

$$
\operatorname{SEN}_a=\frac23,
\qquad
\operatorname{SEN}_b=\frac23,
\qquad
\operatorname{SEN}_c=\frac34.
$$

Wazona czulosc:

$$
\operatorname{SEN}_w=rac{3\cdot\frac23+3\cdot\frac23+4\cdot\frac34}{10}=0.7.
$$

---

## Zdjecie 11 - grupa B, siec 2-1-2 i TSK

### Zadanie 1B - backpropagation dla $w_{1,2}$ i $b_1$

Zbior uczacy:

$$
U=\{(p_1^{(k)},p_2^{(k)},t_4^{(k)},t_5^{(k)}):k=1,\ldots,N\}.
$$

Dla jednego przykladu:

$$
E=0.6e_4^2+0.4e_5^2,
\qquad
e_4=t_4-a_4,
\qquad
e_5=t_5-a_5.
$$

Definiujac lokalny sygnal bledu jako $\delta_i=-\partial E/\partial n_i$:

$$
\begin{aligned}
\delta_4 &= 1.2e_4 f_4'(n_4),\\
\delta_5 &= 0.8e_5 f_5'(n_5),\\
\delta_3 &= f_3'(n_3)(w_{4,3}\delta_4+w_{5,3}\delta_5),\\
\delta_1 &= f_1'(n_1)w_{3,1}\delta_3.
\end{aligned}
$$

Aktualizacja metoda najszybszego spadku:

$$
\boxed{
\begin{aligned}
w_{1,2} &\leftarrow w_{1,2}+\eta\delta_1p_2,\\
b_1 &\leftarrow b_1+\eta\delta_1.
\end{aligned}}
$$

### Zadanie 2B - system TSK

Funkcja:

$$
S(x_1,x_2)=1+x_1-x_2+5x_1x_2,
\qquad
x_1\in[-2,0],\;x_2\in[0,1].
$$

Funkcje przynaleznosci:

$$
N_1(x_1)=\frac{-x_1}{2},
\qquad
P_1(x_1)=\frac{2+x_1}{2},
\qquad
N_2(x_2)=1-x_2,
\qquad
P_2(x_2)=x_2.
$$

Nastepniki regul to wartosci funkcji w wierzcholkach:

$$
\begin{aligned}
q_{NN}&=S(-2,0)=-1, & q_{PN}&=S(0,0)=1,\\
q_{NP}&=S(-2,1)=-12, & q_{PP}&=S(0,1)=0.
\end{aligned}
$$

---

## Zdjecie 12 - widoczne zadanie 2

Siec boolowska z trzema wejsciami:

$$
h_1=\operatorname{step}(a-b+2c+0.5),
\qquad
h_2=\operatorname{step}(a-b+c-0.5),
\qquad
f=\operatorname{step}(h_1+h_2-1.5).
$$

Dla wejsc $0/1$ wyjscie jest rowne $1$ dla mintermow:

$$
001,\;100,\;101,\;111.
$$

Funkcja:

$$
\boxed{
f(a,b,c)=(\neg b\land(a\lor c))\lor(a\land b\land c)
}
$$

Rownowaznie:

$$
f(a,b,c)=(a\land\neg b)\lor(c\land\neg b)\lor(a\land c).
$$

---

## Zdjecie 13 - grupa B, SVM, backpropagation, metryki

### Zadanie 1 - SVM

Dane:

$$
\begin{aligned}
x_1&=(0,0), & y_1&=-1,\\
x_2&=(0,1), & y_2&=1,\\
x_3&=(1,0), & y_3&=1,\\
x_4&=(1,1), & y_4&=-1,
\end{aligned}
\qquad
\sigma=\frac{1}{\sqrt3}.
$$

Dla jadra Gaussa:

$$
K(u,v)=\exp\left(-\frac{\lVert u-v\rVert^2}{2\sigma^2}\right).
$$

Tu $2\sigma^2=2/3$, wiec dla odleglosci kwadratowej $1$ mamy
$r=e^{-3/2}$, a dla odleglosci kwadratowej $2$ mamy $s=e^{-3}$.

Macierz jadra:

$$
K=
\begin{bmatrix}
1 & r & r & s\\
r & 1 & s & r\\
r & s & 1 & r\\
s & r & r & 1
\end{bmatrix}.
$$

Macierz Hessego $H_{ij}=y_iy_jK(x_i,x_j)$:

$$
H=
\begin{bmatrix}
1 & -r & -r & s\\
-r & 1 & s & -r\\
-r & s & 1 & -r\\
s & -r & -r & 1
\end{bmatrix}.
$$

Problem dualny:

$$
\begin{aligned}
\min_{\lambda}\quad & \frac12\lambda^TH\lambda-\mathbf{1}^T\lambda,\\
\text{p.w.}\quad & \sum_i\lambda_iy_i=0,\\
& \lambda_i\ge0.
\end{aligned}
$$

Czyli:

$$
-\lambda_1+\lambda_2+\lambda_3-\lambda_4=0,
\qquad
\lambda_i\ge0.
$$

Jesli formulujemy wersje z miekkim marginesem, dochodzi ograniczenie
$\lambda_i\le C$.

### Zadanie 2 - backpropagation

Zbior uczacy:

$$
U=\{(p_1^{(k)},p_2^{(k)},t_4^{(k)},t_5^{(k)}):k=1,\ldots,N\}.
$$

Dla:

$$
E=\frac14(t_4-a_4)^2+\frac34(t_5-a_5)^2,
\qquad
f_i'(n_i)=\alpha a_i(1-a_i),
$$

lokalne sygnaly bledu:

$$
\begin{aligned}
\delta_4 &= \frac12 e_4\alpha a_4(1-a_4),\\
\delta_5 &= \frac32 e_5\alpha a_5(1-a_5),\\
\delta_3 &= \alpha a_3(1-a_3)(w_{4,3}\delta_4+w_{5,3}\delta_5),\\
\delta_1 &= \alpha a_1(1-a_1)w_{3,1}\delta_3.
\end{aligned}
$$

Aktualizacja:

$$
w_{1,2}\leftarrow w_{1,2}+\eta\delta_1p_2,
\qquad
b_1\leftarrow b_1+\eta\delta_1.
$$

### Zadanie 3 - metryki klasyfikatora binarnego

Dla klasy pozytywnej $b$:

$$
TP=4,
\qquad
FN=2,
\qquad
FP=1,
\qquad
TN=5.
$$

Metryki:

$$
\operatorname{ACC}=\frac{TP+TN}{12}=\frac{9}{12}=0.75,
$$

$$
\operatorname{SEN}=\frac{TP}{TP+FN}=\frac46=\frac23,
\qquad
\operatorname{SPEC}=\frac{TN}{TN+FP}=\frac56.
$$

Gdyby za klase pozytywna przyjac $a$, czulosc i specyficznosc zamieniaja sie
miejscami.

---

## Zdjecie 14 - wariant z komputerami

Dane:

$$
\begin{aligned}
N&=[0.7,0.6,0.1], & D&=[0.9,0.7,0.3],\\
S&=[0.5,0.9,0.8], & G&=[0.1,0.6,0.6],\\
A'&=[0.4,0.5,0.8], & Q_1&=[1,0],\; Q_2=[0,1],\\
y_1&=10, & y_2&=20.
\end{aligned}
$$

Antecedenty:

$$
\begin{aligned}
A_1 &= S\otimes\neg D=[0.0,0.2,0.5],\\
A_2 &= N\oplus G=[0.8,1.0,0.7].
\end{aligned}
$$

Wynik wnioskowania:

$$
B'(y_1)=0.1,
\qquad
B'(y_2)=0.4.
$$

Srodek ciezkosci:

$$
y^*=\frac{10\cdot0.1+20\cdot0.4}{0.1+0.4}=18.
$$

Odpowiedz: nalezy zakupic okolo $18$ komputerow.

---

## Zdjecie 15 - grupa A, budynki i ACC = 0.5

### Zadanie 1A - remont budynku

Dane:

$$
\begin{aligned}
Z&=[0.8,0.9,0.7], & W&=[0.6,0.8,0.5], & D&=[0.6,0.8,0.7],\\
A'&=[1,0.5,0.5], & Q_1&=[1,0,0], & Q_2&=[1,1,0.2],\\
Q_3&=[1,0.5,0.4], & y_1&=24, & y_2&=16,\; y_3=10.
\end{aligned}
$$

Antecedent:

$$
\min(Z,W,D)=[0.6,0.8,0.5].
$$

Wynik wnioskowania:

$$
B'=[1.0,0.3,0.0].
$$

Racjonalne wyostrzenie skladowe:

$$
\begin{aligned}
\text{rano} &= 24\cdot1.0=24,\\
\text{poludnie} &= 16\cdot0.3=4.8,\\
\text{wieczor} &= 10\cdot0.0=0.
\end{aligned}
$$

Odpowiedz: $24$ rano, okolo $5$ w poludnie, $0$ wieczorem.

### Zadanie 2A - ACC i wazona czulosc

Dane:

$$
t=[a,a,b,b,b,c,c,X],
\qquad
p=[a,b,b,a,a,a,c,c],
\qquad
\operatorname{ACC}=0.5.
$$

Bez ostatniego rekordu sa 3 trafienia. Do $\operatorname{ACC}=0.5$ na 8
rekordach potrzeba 4 trafien, wiec:

$$
X=c.
$$

Macierz rozbieznosci:

$$
CM=
\begin{array}{c|ccc}
 & a & b & c\\ \hline
a & 1 & 1 & 0\\
b & 2 & 1 & 0\\
c & 1 & 0 & 2
\end{array}
$$

Wazona czulosc:

$$
\operatorname{SEN}_w=\frac{\text{liczba trafien}}{\text{liczba rekordow}}=\frac48=0.5.
$$

---

## Zdjecie 16 - grupa C

### Zadanie 1C - backpropagation dla $w_{3,1}$ i $b_3$

Zbior uczacy:

$$
U=\{(p_1^{(k)},p_2^{(k)},t_4^{(k)},t_5^{(k)}):k=1,\ldots,N\}.
$$

Dla:

$$
E=0.4e_4^2+0.6e_5^2,
\qquad
e_4=t_4-a_4,
\qquad
e_5=t_5-a_5,
$$

lokalne sygnaly bledu:

$$
\begin{aligned}
\delta_4 &= 0.8e_4f_4'(n_4),\\
\delta_5 &= 1.2e_5f_5'(n_5),\\
\delta_3 &= f_3'(n_3)(w_{4,3}\delta_4+w_{5,3}\delta_5).
\end{aligned}
$$

Aktualizacje:

$$
\boxed{
\begin{aligned}
w_{3,1} &\leftarrow w_{3,1}+\eta\delta_3p_1,\\
b_3 &\leftarrow b_3+\eta\delta_3.
\end{aligned}}
$$

### Zadanie 2C - SVM

Dane:

$$
\begin{aligned}
x_1&=(-1,-1), & y_1&=-1,\\
x_2&=(-1,1), & y_2&=1,\\
x_3&=(1,-1), & y_3&=1,\\
x_4&=(1,1), & y_4&=-1,
\end{aligned}
\qquad
\sigma=\sqrt2.
$$

Tu $2\sigma^2=4$, wiec dla odleglosci kwadratowej $4$ mamy $r=e^{-1}$,
a dla odleglosci kwadratowej $8$ mamy $s=e^{-2}$.

Macierz jadra:

$$
K=
\begin{bmatrix}
1 & r & r & s\\
r & 1 & s & r\\
r & s & 1 & r\\
s & r & r & 1
\end{bmatrix}.
$$

Macierz Hessego:

$$
H=
\begin{bmatrix}
1 & -r & -r & s\\
-r & 1 & s & -r\\
-r & s & 1 & -r\\
s & -r & -r & 1
\end{bmatrix}.
$$

Problem dualny:

$$
\begin{aligned}
\min_{\lambda}\quad & \frac12\lambda^TH\lambda-\mathbf{1}^T\lambda,\\
\text{p.w.}\quad & -\lambda_1+\lambda_2+\lambda_3-\lambda_4=0,\\
& \lambda_i\ge0.
\end{aligned}
$$

W wersji z miekkim marginesem dodatkowo $\lambda_i\le C$.

---

## Zdjecie 19 - grupa A, komputery i siec boolowska

### Zadanie 1A - zakup komputerow

Dane:

$$
\begin{aligned}
N&=[0.9,0.4,0.4], & D&=[1.0,0.6,0.1],\\
S&=[0.7,1.0,0.7], & G&=[1.0,0.2,0.3],\\
A'&=[0.0,0.8,0.2], & Q_1&=[1,0],\; Q_2=[0,1],\\
y_1&=12, & y_2&=24.
\end{aligned}
$$

Antecedenty:

$$
\begin{aligned}
A_1 &= S\otimes\neg D=[0.0,0.4,0.6],\\
A_2 &= N\oplus G=[1.0,0.6,0.7].
\end{aligned}
$$

Wynik wnioskowania:

$$
B'(y_1)=0.2,
\qquad
B'(y_2)=0.4.
$$

Srodek ciezkosci:

$$
y^*=\frac{12\cdot0.2+24\cdot0.4}{0.2+0.4}=20.
$$

Odpowiedz: nalezy zakupic okolo $20$ komputerow.

### Zadanie 2A - siec boolowska

Warstwa pierwsza:

$$
h_1=\operatorname{step}(a-b+0.5),
\qquad
h_2=\operatorname{step}(-a-b-1).
$$

Dla wejsc $0/1$ neuron $h_2$ jest zawsze rowny $0$, wiec:

$$
f=\operatorname{step}(0.5h_1-h_2-0.2)=h_1.
$$

Neuron $h_1$ jest rowny $0$ tylko dla $a=0,b=1$. Funkcja:

$$
\boxed{f(a,b)=a\lor\neg b}.
$$
