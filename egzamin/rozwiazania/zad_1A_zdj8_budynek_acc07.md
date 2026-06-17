# Zadanie 1A (zdjęcie 8) — System ekspertowy: remont budynku (wariant $y_1=60$)

## Treść (skrót)
$X=\{x_1,x_2,x_3\}$ (budynki), wyjścia $y_1=60$ (1. zmiana), $y_2=30$ (2.), $y_3=20$ (3.).
Zbiory rozmyte: $Z=[0.5,0.6,0.7]$, $W=[0.4,0.6,0.3]$, $D=[0.2,0.8,0.6]$.
$Q_1=[1,1,0]$, $Q_2=[1,1,0.2]$, $Q_3=[1,0.5,0.4]$.
Reguły: $R_k: Z\wedge W\wedge D \to Q_k$, $k=1,2,3$ ($\wedge=\min$).
Implikacja Łukasiewicza $a\!\to\!b=\min(1,1-a+b)$; AND/łączenie reguł $\otimes=\max(0,a+b-1)$.
$A'=[1,0.5,0.5]$.

## Krok 1 — wspólny poprzednik $A=\min(Z,W,D)$
$$A(x_1)=\min(0.5,0.4,0.2)=0.2,\ A(x_2)=\min(0.6,0.6,0.8)=0.6,\ A(x_3)=\min(0.7,0.3,0.6)=0.3.$$
$$A=[0.2,\ 0.6,\ 0.3].$$

## Krok 2 — relacje cząstkowe $R_k(x,y)=\min(1,1-A(x)+Q_k(y))$
$$R_1\ (Q_1=[1,1,0]):\quad
\begin{array}{c|ccc}
 & y_1 & y_2 & y_3\\\hline
x_1 & 1 & 1 & 0.8\\
x_2 & 1 & 1 & 0.4\\
x_3 & 1 & 1 & 0.7
\end{array}\qquad
R_2\ (Q_2=[1,1,0.2]):\quad
\begin{array}{c|ccc}
 & y_1 & y_2 & y_3\\\hline
x_1 & 1 & 1 & 1\\
x_2 & 1 & 1 & 0.6\\
x_3 & 1 & 1 & 0.9
\end{array}$$

$$R_3\ (Q_3=[1,0.5,0.4]):\quad
\begin{array}{c|ccc}
 & y_1 & y_2 & y_3\\\hline
x_1 & 1 & 1 & 1\\
x_2 & 1 & 0.9 & 0.8\\
x_3 & 1 & 1 & 1
\end{array}$$

## Krok 3 — relacja globalna $R=R_1\otimes R_2\otimes R_3$ ($\max(0,a+b-1)$)
$$R=\begin{array}{c|ccc}
 & y_1 & y_2 & y_3\\\hline
x_1 & 1 & 1 & 0.8\\
x_2 & 1 & 0.9 & 0\\
x_3 & 1 & 1 & 0.6
\end{array}$$

## Krok 4 — wnioskowanie $B'(y)=\sup_x[A'(x)\otimes R(x,y)]$, $A'=[1,0.5,0.5]$
$$B'(y_1)=\max\{1,\,0.5,\,0.5\}=1,$$
$$B'(y_2)=\max\{1,\,\max(0,0.5+0.9-1),\,0.5\}=\max\{1,0.4,0.5\}=1,$$
$$B'(y_3)=\max\{\max(0,1+0.8-1),\,0,\,\max(0,0.5+0.6-1)\}=\max\{0.8,0,0.1\}=0.8.$$
$$B'=[1,\ 1,\ 0.8].$$

## Krok 5 — wyostrzenie (racjonalne: liczba osób = wartość nominalna $\times$ stopień)
$$\text{rano}=60\cdot1=60,\qquad \text{południe}=30\cdot1=30,\qquad \text{wieczór}=20\cdot0.8=16.$$

$$\boxed{\,\text{rano }60,\quad \text{południe }30,\quad \text{wieczór }16\ \text{pracowników}\,}$$

Trzecia zmiana jest częściowo obsadzona (czynnik $0.8$), bo reguła $R_1$ dopuszczała $Q_1(y_3)=0$, co po złożeniu relacji obniżyło wniosek dla $y_3$.
