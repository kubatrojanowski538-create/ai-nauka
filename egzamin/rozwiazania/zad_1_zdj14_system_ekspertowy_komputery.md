# Zadanie 1 (zdjęcie 14) — Uogólniony system ekspertowy (komputery, $A'=[0.4,0.5,0.8]$)

## Treść (skrót)
$X=\{x_1,x_2,x_3\}$:
$$N=[0.7,0.6,0.1],\ D=[0.9,0.7,0.3],\ S=[0.5,0.9,0.8],\ G=[0.1,0.6,0.6].$$
$Q_1=[1,0]$ ($y_1=10$), $Q_2=[0,1]$ ($y_2=20$).
Reguły: $R_1$: szybkie **i nie** drogie $\Rightarrow Q_1$; $R_2$: niezawodne **lub** z gwarancją $\Rightarrow Q_2$.
Operatory: Łukasiewicz $a\!\to\!b=\min(1,1-a+b)$; OR $\oplus=\min(1,a+b)$; AND/łączenie $\otimes=\max(0,a+b-1)$. Preferencje $A'=[0.4,0.5,0.8]$.

## Krok 1 — poprzedniki
$\lnot D=1-D=[0.1,0.3,0.7]$.
$$A_1=S\otimes\lnot D=\max(0,S+\lnot D-1)=[\,\max(0,-0.4),\max(0,0.2),\max(0,0.5)\,]=[0,0.2,0.5].$$
$$A_2=N\oplus G=\min(1,N+G)=[\min(1,0.8),\min(1,1.2),\min(1,0.7)]=[0.8,1.0,0.7].$$

## Krok 2 — relacje cząstkowe ($R=\min(1,1-A+Q)$)
$$R_1=A_1\!\to\!Q_1\ (Q_1=[1,0]):\quad
\begin{array}{c|cc}
 & y_1 & y_2\\\hline
x_1 & 1 & 1\\
x_2 & 1 & 0.8\\
x_3 & 1 & 0.5
\end{array}\qquad
R_2=A_2\!\to\!Q_2\ (Q_2=[0,1]):\quad
\begin{array}{c|cc}
 & y_1 & y_2\\\hline
x_1 & 0.2 & 1\\
x_2 & 0 & 1\\
x_3 & 0.3 & 1
\end{array}$$

## Krok 3 — relacja globalna $R=R_1\otimes R_2$
$$R=\begin{array}{c|cc}
 & y_1 & y_2\\\hline
x_1 & 0.2 & 1\\
x_2 & 0 & 0.8\\
x_3 & 0.3 & 0.5
\end{array}$$

## Krok 4 — wnioskowanie $B'(y)=\sup_x[A'(x)\otimes R(x,y)]$, $A'=[0.4,0.5,0.8]$
$$B'(y_1)=\max\{\max(0,0.4+0.2-1),\,\max(0,0.5+0-1),\,\max(0,0.8+0.3-1)\}=\max\{0,0,0.1\}=0.1.$$
$$B'(y_2)=\max\{\max(0,0.4+1-1),\,\max(0,0.5+0.8-1),\,\max(0,0.8+0.5-1)\}=\max\{0.4,0.3,0.3\}=0.4.$$
$$B'=[0.1,\ 0.4].$$

## Krok 5 — wyostrzenie (środek ciężkości)
$$y^\*=\frac{10\cdot0.1+20\cdot0.4}{0.1+0.4}=\frac{1+8}{0.5}=\frac{9}{0.5}=18.$$

$$\boxed{\,y^\*=18\ \text{komputerów}\,}$$

Wynik bliski $y_2=20$ — przeważa reguła „kupić więcej" (wyraźnie wyższe $B'(y_2)$).
