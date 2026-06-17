# Zadanie 1A (zdjęcie 15) — System ekspertowy: remont budynku (wariant $y_1=24$)

## Treść (skrót)
Wyjścia: $y_1=24$ (1. zmiana), $y_2=16$ (2.), $y_3=10$ (3.).
Zbiory rozmyte: $Z=[0.8,0.9,0.7]$, $W=[0.6,0.8,0.5]$, $D=[0.6,0.8,0.7]$.
$Q_1=[1,0,0]$, $Q_2=[1,1,0.2]$, $Q_3=[1,0.5,0.4]$.
Reguły $R_k: Z\wedge W\wedge D\to Q_k$; $\wedge=\min$, Łukasiewicz $a\!\to\!b=\min(1,1-a+b)$, $\otimes=\max(0,a+b-1)$. $A'=[1,0.5,0.5]$.

## Krok 1 — poprzednik $A=\min(Z,W,D)$
$$A(x_1)=\min(0.8,0.6,0.6)=0.6,\ A(x_2)=\min(0.9,0.8,0.8)=0.8,\ A(x_3)=\min(0.7,0.5,0.7)=0.5.$$
$$A=[0.6,\ 0.8,\ 0.5].$$

## Krok 2 — relacje cząstkowe $R_k=\min(1,1-A+Q_k)$
$$R_1\ (Q_1=[1,0,0]):\
\begin{array}{c|ccc}
 & y_1 & y_2 & y_3\\\hline
x_1 & 1 & 0.4 & 0.4\\
x_2 & 1 & 0.2 & 0.2\\
x_3 & 1 & 0.5 & 0.5
\end{array}\quad
R_2\ (Q_2=[1,1,0.2]):\
\begin{array}{c|ccc}
 & y_1 & y_2 & y_3\\\hline
x_1 & 1 & 1 & 0.6\\
x_2 & 1 & 1 & 0.4\\
x_3 & 1 & 1 & 0.7
\end{array}\quad
R_3\ (Q_3=[1,0.5,0.4]):\
\begin{array}{c|ccc}
 & y_1 & y_2 & y_3\\\hline
x_1 & 1 & 0.9 & 0.8\\
x_2 & 1 & 0.7 & 0.6\\
x_3 & 1 & 1 & 0.9
\end{array}$$

## Krok 3 — relacja globalna $R=R_1\otimes R_2\otimes R_3$
$$R=\begin{array}{c|ccc}
 & y_1 & y_2 & y_3\\\hline
x_1 & 1 & 0.3 & 0\\
x_2 & 1 & 0 & 0\\
x_3 & 1 & 0.5 & 0.1
\end{array}$$

## Krok 4 — wnioskowanie $B'(y)=\sup_x[A'(x)\otimes R(x,y)]$, $A'=[1,0.5,0.5]$
$$B'(y_1)=\max\{1,\,0.5,\,0.5\}=1,$$
$$B'(y_2)=\max\{\max(0,1+0.3-1),\,0,\,\max(0,0.5+0.5-1)\}=\max\{0.3,0,0\}=0.3,$$
$$B'(y_3)=\max\{0,\,0,\,\max(0,0.5+0.1-1)\}=0.$$
$$B'=[1,\ 0.3,\ 0].$$

## Krok 5 — wyostrzenie (liczba osób = wartość nominalna $\times$ stopień)
$$\text{rano}=24\cdot1=24,\qquad \text{południe}=16\cdot0.3\approx5,\qquad \text{wieczór}=10\cdot0=0.$$

$$\boxed{\,\text{rano }24,\quad \text{południe }\approx5,\quad \text{wieczór }0\ \text{pracowników}\,}$$

Pierwsza zmiana jest w pełni obsadzona, druga w niewielkim stopniu, a trzecia zmiana w ogóle nie jest potrzebna (relacja globalna wygasiła wyjście $y_3$).
