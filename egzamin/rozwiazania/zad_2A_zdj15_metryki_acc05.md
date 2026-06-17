# Zadanie 2A (zdjęcie 15) — Metryki klasyfikatora, brakująca etykieta $X$ (ACC=0.5)

## Treść (skrót)
$$t=[a,a,b,b,b,c,c,X],\qquad p=[a,b,b,a,a,a,c,c].$$
Dokładność $ACC=0.5$. Wyznaczyć $X$ oraz ważoną czułość $SEN$.

## Krok 1 — wyznaczenie $X$
$ACC=0.5$ przy 8 próbkach → **4 trafienia**. Pozycje 1–7:

| # | 1 | 2 | 3 | 4 | 5 | 6 | 7 |
|---|---|---|---|---|---|---|---|
| $t$ | a | a | b | b | b | c | c |
| $p$ | a | b | b | a | a | a | c |
| zgodność | ✓ | ✗ | ✓ | ✗ | ✗ | ✗ | ✓ |

Trafień w 1–7: **3**. Aby było 4, pozycja 8 musi być trafna:
$$X=p_8=c\quad\Rightarrow\quad \boxed{X=c}.$$

## Krok 2 — macierz pomyłek
Pełne: $t=[a,a,b,b,b,c,c,c]$, $p=[a,b,b,a,a,a,c,c]$.

| $t\backslash p$ | a | b | c | support |
|---|---|---|---|---|
| **a** | 1 | 1 | 0 | 2 |
| **b** | 2 | 1 | 0 | 3 |
| **c** | 1 | 0 | 2 | 3 |

(Przekątna $1+1+2=4$ → $ACC=4/8=0.5$ ✓.)

## Krok 3 — czułość dla każdej klasy
$$SEN_a=\frac12=0.5,\qquad SEN_b=\frac13\approx0.333,\qquad SEN_c=\frac23\approx0.667.$$

## Krok 4 — ważona czułość
$$SEN_{\text{w}}=\frac{2\cdot\frac12+3\cdot\frac13+3\cdot\frac23}{8}=\frac{1+1+2}{8}=\frac48=0.5.$$

$$\boxed{\,X=c,\qquad SEN_{\text{ważona}}=0.5\,}$$

Ponownie potwierdza się tożsamość $SEN_{\text{ważona}}=ACC$ (suma trafień podzielona przez liczbę próbek).
