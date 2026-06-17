# Zadanie 3 (zdjęcie 13) — Dokładność, czułość i specyficzność klasyfikatora binarnego

## Treść (skrót)
12 rekordów testowych (klasy $a$, $b$):

| # | rzecz. | predykcja | | # | rzecz. | predykcja |
|---|---|---|---|---|---|---|
| 1 | a | a | | 7 | b | b |
| 2 | a | a | | 8 | b | a |
| 3 | b | a | | 9 | a | a |
| 4 | a | b | | 10 | b | b |
| 5 | a | a | | 11 | a | a |
| 6 | b | b | | 12 | b | b |

## Krok 1 — macierz pomyłek
Przyjmujemy klasę $a$ jako **pozytywną**, $b$ jako negatywną.

Próbki prawdziwej klasy $a$: #1,2,4,5,9,11 (6 szt.) → predykcje $a$: 1,2,5,9,11 (5), $b$: 4 (1).
Próbki prawdziwej klasy $b$: #3,6,7,8,10,12 (6 szt.) → predykcje $b$: 6,7,10,12 (4), $a$: 3,8 (2).

|  | pred. $a$ (P) | pred. $b$ (N) |
|---|---|---|
| **rzecz. $a$ (P)** | TP = 5 | FN = 1 |
| **rzecz. $b$ (N)** | FP = 2 | TN = 4 |

## Krok 2 — metryki
**Dokładność (ACC):**
$$ACC=\frac{TP+TN}{N}=\frac{5+4}{12}=\frac{9}{12}=0.75.$$

**Czułość (SEN, recall, TPR):**
$$SEN=\frac{TP}{TP+FN}=\frac{5}{6}\approx0.833.$$

**Specyficzność (SPEC, TNR):**
$$SPEC=\frac{TN}{TN+FP}=\frac{4}{6}\approx0.667.$$

$$\boxed{\,ACC=0.75,\qquad SEN=\tfrac56\approx0.833,\qquad SPEC=\tfrac46\approx0.667\,}$$

> Uwaga: gdyby przyjąć klasę $b$ jako pozytywną, wartości czułości i specyficzności zamieniają się miejscami: $SEN=4/6$, $SPEC=5/6$; dokładność pozostaje $0.75$.
