# Zadanie 1 (grupa A1/B1) — Nawigacja robota, system Takagi–Sugeno

## Treść (skrót)
Sygnały wejściowe: $z_1=\max(x_1,x_2)$ (prawo), $z_2=\max(x_3,x_4)$ (lewo), $z_3=\max(x_5,x_6)$ (przód). Zbiory rozmyte:
$$N_i(z_i)=1-\frac{z_i}{a},\qquad P_i(z_i)=1-N_i(z_i)=\frac{z_i}{a}.$$
Reguły (następniki dla $(u_L,u_R)$):

| Reg. | $z_1$ | $z_2$ | $z_3$ | $(u_L,u_R)$ |
|---|---|---|---|---|
| $R_1$ | $N_1$ | $N_2$ | $N_3$ | $(C,C)$ |
| $R_2$ | $P_1$ | $N_2$ | $N_3$ | $(-C,C)$ |
| $R_3$ | $N_1$ | $P_2$ | $N_3$ | $(C,-C)$ |
| $R_4$ | $P_1$ | $P_2$ | $N_3$ | $(C,C)$ |
| $R_5$ | $N_1$ | $N_2$ | $P_3$ | $(-C,C)$ |
| $R_6$ | $P_1$ | $N_2$ | $P_3$ | $(-C,C)$ |
| $R_7$ | $N_1$ | $P_2$ | $P_3$ | $(C,-C)$ |
| $R_8$ | $P_1$ | $P_2$ | $P_3$ | $(-C,C)$ |

Wskazania: $x_1=0.9a,\ x_2=0.8a,\ x_3=0.2a,\ x_4=0.1a,\ x_5=x_6=0$. Stosować **tylko** wzór TS:
$$S=\frac{\sum_{i,j,k=0}^1 m_{ijk}q_{ijk}}{\sum_{i,j,k=0}^1 m_{ijk}},\qquad \sum m_{ijk}=1.$$

## Krok 1 — sygnały wejściowe
$$z_1=\max(0.9a,0.8a)=0.9a,\quad z_2=\max(0.2a,0.1a)=0.2a,\quad z_3=\max(0,0)=0.$$

## Krok 2 — przynależności
$$N_1=1-0.9=0.1,\ P_1=0.9;\qquad N_2=1-0.2=0.8,\ P_2=0.2;\qquad N_3=1-0=1,\ P_3=0.$$

Ponieważ $P_3=0$, **wszystkie reguły $R_5\!-\!R_8$ (z $P_3$) mają zerowe dopasowanie**.

## Krok 3 — stopnie dopasowania reguł aktywnych
Indeksowanie: $i\!: N_1/P_1$, $j\!: N_2/P_2$, $k\!: N_3/P_3$.
$$
\begin{aligned}
m_{000}&=N_1N_2N_3=0.1\cdot0.8\cdot1=0.08 &(R_1)\\
m_{100}&=P_1N_2N_3=0.9\cdot0.8\cdot1=0.72 &(R_2)\\
m_{010}&=N_1P_2N_3=0.1\cdot0.2\cdot1=0.02 &(R_3)\\
m_{110}&=P_1P_2N_3=0.9\cdot0.2\cdot1=0.18 &(R_4)
\end{aligned}
$$
Suma: $0.08+0.72+0.02+0.18=1$ ✓ (mianownik = 1).

## Krok 4 — wyjścia (liczba impulsów)
**Lewe koło** ($q_L$: $R_1\!=\!C,R_2\!=\!-C,R_3\!=\!C,R_4\!=\!C$):
$$u_L=C(0.08-0.72+0.02+0.18)=-0.44\,C.$$

**Prawe koło** ($q_R$: $R_1\!=\!C,R_2\!=\!C,R_3\!=\!-C,R_4\!=\!C$):
$$u_R=C(0.08+0.72-0.02+0.18)=0.96\,C.$$

$$\boxed{\,u_L=-0.44\,C,\qquad u_R=0.96\,C\,}$$

## Weryfikacja (wzorami z wykładu — których nie wolno było użyć, ale dla kontroli)
$$u_R=\tfrac{C}{a^2}(a^2-2az_2+2z_1z_2)=C(1-0.4+0.36)=0.96C\ \checkmark$$
$$u_L=\tfrac{C}{a^3}(a^3-2a^2z_1+2az_1z_2)=C(1-1.8+0.36)=-0.44C\ \checkmark$$

**Interpretacja:** przeszkoda po prawej (duże $z_1$) → robot skręca w prawo: lewe koło cofa ($u_L<0$), prawe jedzie naprzód ($u_R>0$).
