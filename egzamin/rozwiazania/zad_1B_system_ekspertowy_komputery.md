# Zadanie 1B (zdjęcie 3) — Uogólniony system ekspertowy (zakup komputerów)

## Treść (skrót)
$X=\{x_1,x_2,x_3\}$, zbiory rozmyte:
$$N=[0.4,0.5,0.9]^T,\ D=[0.6,0.4,1.0]^T,\ S=[0.8,0.6,0.9]^T,\ G=[0.2,0.4,0.6]^T.$$
$Y=\{y_1,y_2\}$, $Q_1=[1,0]$ ($y_1=10$ szt.), $Q_2=[0,1]$ ($y_2=16$ szt.).
Reguły: $R_1$: szybkie **i nie** drogie $\Rightarrow Q_1$; $R_2$: niezawodne **lub** z gwarancją $\Rightarrow Q_2$.
Operatory: implikacja Łukasiewicza $a\!\to\!b=\min(1,1-a+b)$; OR $a\oplus b=\min(1,a+b)$; AND/łączenie reguł $a\otimes b=\max(0,a+b-1)$.
Preferencje: $A'=[0.7,0.1,0.2]^T$.

> Uwaga: reguła $R_1$ to *szybkie i NIE drogie*, więc poprzednik to $S\otimes \lnot D$ (w treści wskazówki zapisano skrótowo $S\otimes D$, ale słowny opis jednoznacznie mówi „nie są drogie").

## Krok 1 — poprzedniki reguł
$\lnot D=1-D=[0.4,0.6,0.0]$.
$$A_1=S\otimes\lnot D=\max(0,S+\lnot D-1)=[\,\max(0,0.2),\max(0,0.2),\max(0,-0.1)\,]=[0.2,0.2,0].$$
$$A_2=N\oplus G=\min(1,N+G)=[\min(1,0.6),\min(1,0.9),\min(1,1.5)]=[0.6,0.9,1.0].$$

## Krok 2 — relacje cząstkowe (implikacja Łukasiewicza $R(x,y)=\min(1,1-A(x)+Q(y))$)
$$R_1=A_1\!\to\!Q_1\ (Q_1=[1,0]):\quad
\begin{array}{c|cc}
 & y_1 & y_2\\\hline
x_1 & 1 & 0.8\\
x_2 & 1 & 0.8\\
x_3 & 1 & 1
\end{array}$$

$$R_2=A_2\!\to\!Q_2\ (Q_2=[0,1]):\quad
\begin{array}{c|cc}
 & y_1 & y_2\\\hline
x_1 & 0.4 & 1\\
x_2 & 0.1 & 1\\
x_3 & 0 & 1
\end{array}$$

## Krok 3 — relacja globalna $R=R_1\otimes R_2$ (element po elemencie $\max(0,a+b-1)$)
$$R=\begin{array}{c|cc}
 & y_1 & y_2\\\hline
x_1 & 0.4 & 0.8\\
x_2 & 0.1 & 0.8\\
x_3 & 0 & 1
\end{array}$$

## Krok 4 — wnioskowanie $B'(y)=\sup_x[A'(x)\otimes R(x,y)]$, $A'=[0.7,0.1,0.2]$
$$B'(y_1)=\max\{\max(0,0.7+0.4-1),\,\max(0,0.1+0.1-1),\,\max(0,0.2+0-1)\}=\max\{0.1,0,0\}=0.1.$$
$$B'(y_2)=\max\{\max(0,0.7+0.8-1),\,\max(0,0.1+0.8-1),\,\max(0,0.2+1-1)\}=\max\{0.5,0,0.2\}=0.5.$$
$$B'=[0.1,\ 0.5].$$

## Krok 5 — wyostrzenie (środek ciężkości)
$$y^\*=\frac{y_1 B'(y_1)+y_2 B'(y_2)}{B'(y_1)+B'(y_2)}=\frac{10\cdot0.1+16\cdot0.5}{0.1+0.5}=\frac{1+8}{0.6}=\frac{9}{0.6}=15.$$

$$\boxed{\,y^\*=15\ \text{komputerów}\,}$$

Wynik (15) leży między $y_1=10$ a $y_2=16$, z przewagą reguły $R_2$ (kup więcej) — zgodnie z silniejszym dopasowaniem $B'(y_2)=0.5$.
