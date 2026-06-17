# Zadanie 1D — System Takagi–Sugeno (uproszczona postać)

## Treść (skrót)
System TS ma wejścia $x\in[-a,a]$, $y\in[-b,b]$ i wyjście $S$. Funkcje przynależności są liniowe i komplementarne:
$$N_1(x)=\frac{a-x}{2a},\quad P_1(x)=1-N_1(x)=\frac{a+x}{2a},$$
$$N_2(y)=\frac{b-y}{2b},\quad P_2(y)=1-N_2(y)=\frac{b+y}{2b}.$$
Reguły:
- $R_1$: $N_1\wedge N_2 \Rightarrow S=4ab$
- $R_2$: $P_1\wedge N_2 \Rightarrow S=-4ab$
- $R_3$: $N_1\wedge P_2 \Rightarrow S=4ab$
- $R_4$: $P_1\wedge P_2 \Rightarrow S=8ab$

Należy podać najprostszą postać funkcji $S(x,y)$.

## Rozwiązanie
W systemie TS wyjście jest średnią ważoną następników, z wagami równymi stopniom dopasowania reguł $m_i$ (iloczyny przynależności):
$$S=\frac{\sum_i m_i q_i}{\sum_i m_i}.$$

**Mianownik = 1.** Ponieważ przynależności są komplementarne:
$$\sum_i m_i=(N_1+P_1)(N_2+P_2)=1\cdot 1=1.$$
Zatem
$$S=4ab\,N_1N_2-4ab\,P_1N_2+4ab\,N_1P_2+8ab\,P_1P_2.$$

Podstawiając przynależności (czynnik $4ab$ skraca się z mianownikami $4ab$, $8ab$ daje $2$):
$$
\begin{aligned}
S&=(a-x)(b-y)-(a+x)(b-y)+(a-x)(b+y)+2(a+x)(b+y).
\end{aligned}
$$

Rozwijając i grupując wyrazy:

| składnik | $ab$ | $ay$ | $bx$ | $xy$ |
|---|---|---|---|---|
| $(a-x)(b-y)$ | $+1$ | $-1$ | $-1$ | $+1$ |
| $-(a+x)(b-y)$ | $-1$ | $+1$ | $-1$ | $+1$ |
| $(a-x)(b+y)$ | $+1$ | $+1$ | $-1$ | $-1$ |
| $2(a+x)(b+y)$ | $+2$ | $+2$ | $+2$ | $+2$ |
| **suma** | $3$ | $3$ | $-1$ | $3$ |

$$\boxed{\,S(x,y)=3ab-bx+3ay+3xy\,}$$

## Weryfikacja w narożnikach
- $(-a,-b)$ (czysto $R_1$): $3ab+ab-3ab+3ab=4ab$ ✓
- $(a,-b)$ ($R_2$): $3ab-ab-3ab-3ab=-4ab$ ✓
- $(-a,b)$ ($R_3$): $3ab+ab+3ab-3ab=4ab$ ✓
- $(a,b)$ ($R_4$): $3ab-ab+3ab+3ab=8ab$ ✓

Funkcja jest dwuliniowa (multilinear) w $x,y$, co jest typowe dla systemu TS z liniowymi, komplementarnymi przynależnościami.
