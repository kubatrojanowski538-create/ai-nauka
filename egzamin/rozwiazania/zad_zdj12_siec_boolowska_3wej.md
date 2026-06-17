# Zadanie 2 (zdjęcie 12) — Funkcja boolowska realizowana przez sieć (3 wejścia)

## Treść (skrót)
Dwuwarstwowa sieć, aktywacje skokowe $f(x)=0$ dla $x<0$, $f(x)=1$ dla $x\ge0$.
Warstwa 1 (neurony 1, 2), **3 wejścia**:
$$w_{11}=1,\ w_{12}=-1,\ w_{13}=2,\ b_1=0.5;\qquad w_{21}=1,\ w_{22}=-1,\ w_{23}=1,\ b_2=-0.5.$$
Warstwa 2 (neuron 3): $w_{31}=1,\ w_{32}=1,\ b_3=-1.5$.
Jaką funkcję boolowską realizuje sieć?

## Krok 1 — sygnały warstwy 1 (oznaczamy wejścia $a,b,c$)
$$n_1=a-b+2c+0.5,\qquad n_2=a-b+c-0.5.$$

## Krok 2 — neuron wyjściowy 3 to AND
$$n_3=a_1+a_2-1.5.$$
$a_3=1$ tylko gdy $a_1=a_2=1$ ($1+1-1.5=0.5\ge0$); gdy choć jedno $=0$, $n_3\le-0.5<0$. Zatem $a_3=a_1\wedge a_2$.

## Krok 3 — tablica prawdy

| $a$ | $b$ | $c$ | $n_1$ | $a_1$ | $n_2$ | $a_2$ | $a_3=a_1\wedge a_2$ |
|---|---|---|---|---|---|---|---|
| 0 | 0 | 0 | 0.5 | 1 | -0.5 | 0 | 0 |
| 0 | 0 | 1 | 2.5 | 1 | 0.5 | 1 | 1 |
| 0 | 1 | 0 | -0.5 | 0 | -1.5 | 0 | 0 |
| 0 | 1 | 1 | 1.5 | 1 | -0.5 | 0 | 0 |
| 1 | 0 | 0 | 1.5 | 1 | 0.5 | 1 | 1 |
| 1 | 0 | 1 | 3.5 | 1 | 1.5 | 1 | 1 |
| 1 | 1 | 0 | 0.5 | 1 | -0.5 | 0 | 0 |
| 1 | 1 | 1 | 2.5 | 1 | 0.5 | 1 | 1 |

Zauważmy, że wszędzie tam, gdzie $a_2=1$, jest też $a_1=1$, więc $a_3=a_2$. Neuron 2 zapala się, gdy $a-b+c\ge1$.

## Krok 4 — postać funkcji
Wyjście $=1$ dla minteremów $001,100,101,111$, tzn. gdy $a-b+c\ge1$:
- jeśli $b=0$: warunek $a+c\ge1$, czyli $a\vee c$;
- jeśli $b=1$: warunek $a+c\ge2$, czyli $a\wedge c$.

$$\boxed{\,f(a,b,c)=\big(\lnot b\wedge(a\vee c)\big)\ \vee\ (a\wedge b\wedge c)\,}$$

Równoważnie (postać sum minteremów / Karnaugh):
$$f=(a\wedge\lnot b)\vee(c\wedge\lnot b)\vee(a\wedge c).$$

Funkcja zwraca 1, gdy „przewaga" wejść $a,c$ nad $b$ jest dodatnia ($a-b+c\ge1$).
