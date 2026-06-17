# Zadanie 2A (zdjęcie 8) — Metryki klasyfikatora, brakująca etykieta $Y$ (ACC=0.7)

## Treść (skrót)
Etykiety prawdziwe i predykcje (klasy $\{a,b,c\}$):
$$t=[a,a,a,b,b,c,c,c,b,Y],\qquad p=[a,c,a,b,a,c,c,b,b,c].$$
Dokładność $ACC=0.7$. Wyznaczyć $Y$ oraz ważoną czułość $SEN$.

## Krok 1 — wyznaczenie $Y$
$ACC=0.7$ przy 10 próbkach → **7 trafień**. Sprawdzamy pozycje 1–9:

| # | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|---|---|---|---|---|---|---|---|---|---|
| $t$ | a | a | a | b | b | c | c | c | b |
| $p$ | a | c | a | b | a | c | c | b | b |
| zgodność | ✓ | ✗ | ✓ | ✓ | ✗ | ✓ | ✓ | ✗ | ✓ |

Trafień w 1–9: **6**. Aby było 7, pozycja 10 musi być trafna:
$$Y=p_{10}=c\quad\Rightarrow\quad \boxed{Y=c}.$$

## Krok 2 — macierz pomyłek (confusion matrix)
Pełne wektory: $t=[a,a,a,b,b,c,c,c,b,c]$, $p=[a,c,a,b,a,c,c,b,b,c]$.

Wiersze = klasa prawdziwa, kolumny = predykcja:

| $t\backslash p$ | a | b | c | suma (support) |
|---|---|---|---|---|
| **a** | 2 | 0 | 1 | 3 |
| **b** | 1 | 2 | 0 | 3 |
| **c** | 0 | 1 | 3 | 4 |

(Sprawdzenie: na przekątnej $2+2+3=7$ trafień → $ACC=7/10=0.7$ ✓.)

## Krok 3 — czułość (recall) dla każdej klasy
$$SEN_a=\frac{2}{3},\qquad SEN_b=\frac{2}{3},\qquad SEN_c=\frac{3}{4}.$$

## Krok 4 — ważona czułość (waga = liczność klasy)
$$SEN_{\text{w}}=\frac{n_a\,SEN_a+n_b\,SEN_b+n_c\,SEN_c}{N}
=\frac{3\cdot\frac23+3\cdot\frac23+4\cdot\frac34}{10}=\frac{2+2+3}{10}=0.7.$$

$$\boxed{\,Y=c,\qquad SEN_{\text{ważona}}=0.7\,}$$

**Uwaga:** ważona czułość zawsze równa się dokładności, bo
$SEN_\text{w}=\frac1N\sum_k n_k\frac{TP_k}{n_k}=\frac{\sum_k TP_k}{N}=ACC.$
