# Zadanie 1A (zdjęcie 19) — Uogólniony system ekspertowy (komputery, $A'=[0,0.8,0.2]$)

## Treść (skrót)
$X=\{x_1,x_2,x_3\}$:
$$N=[0.9,0.4,0.4],\ D=[1.0,0.6,0.1],\ S=[0.7,1.0,0.7],\ G=[1.0,0.2,0.3].$$
$Q_1=[1,0]$ ($y_1=12$), $Q_2=[0,1]$ ($y_2=24$).
Reguły: $R_1$: szybkie **i nie** drogie $\Rightarrow Q_1$; $R_2$: niezawodne **lub** z gwarancją $\Rightarrow Q_2$.
Operatory jak w pozostałych zadaniach z systemem uogólnionym. Preferencje $A'=[0,0.8,0.2]$.

## Krok 1 — poprzedniki
$\lnot D=1-D=[0,0.4,0.9]$.
$$A_1=S\otimes\lnot D=\max(0,S+\lnot D-1)=[\,\max(0,-0.3),\max(0,0.4),\max(0,0.6)\,]=[0,0.4,0.6].$$
$$A_2=N\oplus G=\min(1,N+G)=[\min(1,1.9),\min(1,0.6),\min(1,0.7)]=[1.0,0.6,0.7].$$

## Krok 2 — relacje cząstkowe ($R=\min(1,1-A+Q)$)
$$R_1=A_1\!\to\!Q_1\ (Q_1=[1,0]):\quad
\begin{array}{c|cc}
 & y_1 & y_2\\\hline
x_1 & 1 & 1\\
x_2 & 1 & 0.6\\
x_3 & 1 & 0.4
\end{array}\qquad
R_2=A_2\!\to\!Q_2\ (Q_2=[0,1]):\quad
\begin{array}{c|cc}
 & y_1 & y_2\\\hline
x_1 & 0 & 1\\
x_2 & 0.4 & 1\\
x_3 & 0.3 & 1
\end{array}$$

## Krok 3 — relacja globalna $R=R_1\otimes R_2$
$$R=\begin{array}{c|cc}
 & y_1 & y_2\\\hline
x_1 & 0 & 1\\
x_2 & 0.4 & 0.6\\
x_3 & 0.3 & 0.4
\end{array}$$

## Krok 4 — wnioskowanie $B'(y)=\sup_x[A'(x)\otimes R(x,y)]$, $A'=[0,0.8,0.2]$
$$B'(y_1)=\max\{\max(0,0+0-1),\,\max(0,0.8+0.4-1),\,\max(0,0.2+0.3-1)\}=\max\{0,0.2,0\}=0.2.$$
$$B'(y_2)=\max\{\max(0,0+1-1),\,\max(0,0.8+0.6-1),\,\max(0,0.2+0.4-1)\}=\max\{0,0.4,0\}=0.4.$$
$$B'=[0.2,\ 0.4].$$

## Krok 5 — wyostrzenie (środek ciężkości)
$$y^\*=\frac{12\cdot0.2+24\cdot0.4}{0.2+0.4}=\frac{2.4+9.6}{0.6}=\frac{12}{0.6}=20.$$

$$\boxed{\,y^\*=20\ \text{komputerów}\,}$$

Wynik (20) leży między $y_1=12$ a $y_2=24$, bliżej $y_2$ — silniejsza okazała się reguła $R_2$ (kup więcej).
