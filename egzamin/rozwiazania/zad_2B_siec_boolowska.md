# Zadanie 2B (zdjęcia 3/6) — Funkcja boolowska realizowana przez sieć

## Treść (skrót)
Dwuwarstwowa sieć z funkcjami aktywacji skokowymi $f(x)=0$ dla $x<0$, $f(x)=1$ dla $x\ge0$.
Warstwa 1 (neurony 1, 2): $w_{11}=2,\ w_{12}=1,\ b_1=-0.3,\quad w_{21}=-1,\ w_{22}=0,\ b_2=-3$.
Warstwa 2 (neuron 3): $w_{31}=5,\ w_{32}=-1,\ b_3=-0.2$.
($w_{ij}$ — waga neuronu $i$ od wejścia $j$.) Wejścia $p_1,p_2\in\{0,1\}$.

## Krok 1 — neuron 2 jest stale wyłączony
$$n_2=-p_1+0\cdot p_2-3=-p_1-3.$$
Dla $p_1\in\{0,1\}$: $n_2\in\{-3,-4\}<0\ \Rightarrow\ a_2=0$ zawsze.

## Krok 2 — neuron 1
$$a_1=f(2p_1+p_2-0.3).$$

| $p_1$ | $p_2$ | $n_1$ | $a_1$ |
|---|---|---|---|
| 0 | 0 | $-0.3$ | 0 |
| 0 | 1 | $0.7$ | 1 |
| 1 | 0 | $1.7$ | 1 |
| 1 | 1 | $2.7$ | 1 |

## Krok 3 — neuron wyjściowy 3
$$n_3=5a_1-a_2-0.2=5a_1-0.2\quad(\text{bo }a_2=0).$$
- $a_1=0\Rightarrow n_3=-0.2<0\Rightarrow a_3=0$
- $a_1=1\Rightarrow n_3=4.8\ge0\Rightarrow a_3=1$

Czyli $a_3=a_1$.

## Wynik — tablica prawdy

| $p_1$ | $p_2$ | wyjście $a_3$ |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 1 |

$$\boxed{\,f(p_1,p_2)=p_1\ \mathbf{OR}\ p_2\,}$$

Sieć realizuje **sumę logiczną (OR)**. Neuron 1 wykrywa „przynajmniej jedno wejście aktywne" (przesunięcie $-0.3$ z wagami $2$ i $1$), neuron 2 jest nieaktywny, a neuron wyjściowy jedynie przepisuje sygnał neuronu 1.
