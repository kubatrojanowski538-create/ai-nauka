# Zadanie 2A (zdjęcie 19) — Funkcja boolowska realizowana przez sieć

## Treść (skrót)
Dwuwarstwowa sieć, aktywacje skokowe $f(x)=0$ dla $x<0$, $f(x)=1$ dla $x\ge0$.
Warstwa 1 (neurony 1, 2): $w_{11}=1,\ w_{12}=-1,\ b_1=0.5;\quad w_{21}=-1,\ w_{22}=-1,\ b_2=-1$.
Warstwa 2 (neuron 3): $w_{31}=0.5,\ w_{32}=-1,\ b_3=-0.2$. Wejścia $p_1,p_2\in\{0,1\}$ (oznaczane $a,b$).

## Krok 1 — neuron 2 jest stale wyłączony
$$n_2=-a-b-1.$$
Dla $a,b\in\{0,1\}$: $n_2\in\{-1,-2,-3\}<0\ \Rightarrow\ a_2=0$ zawsze.

## Krok 2 — neuron 1
$$a_1=f(a-b+0.5).$$

| $a$ | $b$ | $n_1$ | $a_1$ |
|---|---|---|---|
| 0 | 0 | 0.5 | 1 |
| 0 | 1 | -0.5 | 0 |
| 1 | 0 | 1.5 | 1 |
| 1 | 1 | 0.5 | 1 |

## Krok 3 — neuron wyjściowy 3
$$n_3=0.5\,a_1-a_2-0.2=0.5\,a_1-0.2\quad(\text{bo }a_2=0).$$
- $a_1=0\Rightarrow n_3=-0.2<0\Rightarrow a_3=0$
- $a_1=1\Rightarrow n_3=0.3\ge0\Rightarrow a_3=1$

Czyli $a_3=a_1$.

## Wynik — tablica prawdy

| $a$ | $b$ | wyjście $a_3$ |
|---|---|---|
| 0 | 0 | 1 |
| 0 | 1 | 0 |
| 1 | 0 | 1 |
| 1 | 1 | 1 |

Wyjście $=0$ tylko dla $(a,b)=(0,1)$.

$$\boxed{\,f(a,b)=a\ \vee\ \lnot b\,}$$

Równoważnie jest to **implikacja** $b\Rightarrow a$ (prawda zawsze poza przypadkiem $b=1,a=0$). Neuron 1 realizuje warunek $a-b+0.5\ge0$, a neuron wyjściowy jedynie go przepisuje.
