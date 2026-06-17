# Zadanie 1F (zdjęcia 5/9) — Algorytm GEP, stopień dopasowania chromosomu

## Treść (skrót)
Funkcja docelowa $f(a,b,c)=(a\wedge\lnot b)\vee(b\wedge c)$.
Funkcje: $\text{AND}=A$, $\text{OR}=O$, $\text{NOT}=N$; terminale $a,b,c$; 2 geny, długość genu 11 (głowa 5, ogon 6), łączenie genów: OR.
Chromosom: **Gen 1:** `OANabcaNbca`, **Gen 2:** `AOcbaabcabb`. Obliczyć stopień dopasowania (dokładność) do $f$.

## Krok 1 — dekodowanie K-wyrażeń (Karva)
Drzewo czyta się wszerz (poziomami), pobierając tylu argumentów ile wynosi arność symbolu.

**Gen 1:** `O A N a b c a N b c a`
- korzeń `O` (arność 2) → dzieci: `A`, `N`
- `A` (arność 2) → dzieci: `a`, `b`; `N` (arność 1) → dziecko: `c`
- wyrażenie: $\;O(A(a,b),\,N(c)) = (a\wedge b)\vee\lnot c$

**Gen 2:** `A O c b a a b c a b b`
- korzeń `A` (arność 2) → dzieci: `O`, `c`
- `O` (arność 2) → dzieci: `b`, `a`; `c` — terminal
- wyrażenie: $\;A(O(b,a),\,c) = (a\vee b)\wedge c$

## Krok 2 — łączenie genów operatorem OR
$$g(a,b,c)=\big[(a\wedge b)\vee\lnot c\big]\ \vee\ \big[(a\vee b)\wedge c\big].$$

## Krok 3 — tablice prawdy i porównanie
$f=(a\wedge\lnot b)\vee(b\wedge c)$ vs. chromosom $g$:

| $a$ | $b$ | $c$ | $f$ | $g$ | zgodność |
|---|---|---|---|---|---|
| 0 | 0 | 0 | 0 | 1 | ✗ |
| 0 | 0 | 1 | 0 | 0 | ✓ |
| 0 | 1 | 0 | 0 | 1 | ✗ |
| 0 | 1 | 1 | 1 | 1 | ✓ |
| 1 | 0 | 0 | 1 | 1 | ✓ |
| 1 | 0 | 1 | 1 | 1 | ✓ |
| 1 | 1 | 0 | 0 | 1 | ✗ |
| 1 | 1 | 1 | 1 | 1 | ✓ |

Wyjaśnienie wartości $g$: składnik $\lnot c$ zapala $g$ dla wszystkich przypadków z $c=0$ (stąd nadmiarowe jedynki w wierszach 000, 010, 110).

## Krok 4 — stopień dopasowania (dokładność)
Liczba zgodnych przypadków: 5 z 8.
$$\boxed{\ \text{fitness}=\frac{5}{8}=0.625=62.5\%\ }$$

Chromosom poprawnie odtwarza 5 z 8 wartości funkcji logicznej — osiągnięta dokładność na tym etapie ewolucji to **62,5%**.
