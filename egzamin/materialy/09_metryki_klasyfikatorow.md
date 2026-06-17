# 9. Ocena klasyfikatorów — macierz pomyłek i metryki

## 9.1. Macierz pomyłek (confusion matrix, CM)
Wiersze = klasa rzeczywista, kolumny = predykcja. Element $CM_{ij}$ = liczba próbek klasy $i$ zaklasyfikowanych jako $j$. Na przekątnej — trafienia.

Dla klasyfikatora **binarnego** (klasa pozytywna P, negatywna N):
|  | pred. P | pred. N |
|---|---|---|
| rzecz. P | TP | FN |
| rzecz. N | FP | TN |

## 9.2. Podstawowe metryki
$$ACC=\frac{TP+TN}{TP+TN+FP+FN}=\frac{\text{trafienia}}{\text{wszystkie}},$$
$$SEN=TPR=\frac{TP}{TP+FN}\ (\text{czułość, recall}),\qquad
SPEC=TNR=\frac{TN}{TN+FP}\ (\text{specyficzność}).$$
Dodatkowo: precyzja $PPV=\dfrac{TP}{TP+FP}$, $F_1=\dfrac{2\,PPV\cdot SEN}{PPV+SEN}$.

## 9.3. Wiele klas — czułość ważona
Czułość klasy $k$: $SEN_k=\dfrac{TP_k}{\text{liczność klasy }k}$ (przekątna / suma wiersza).
**Czułość ważona** (waga = liczność klasy $n_k$):
$$SEN_{\text{w}}=\frac{\sum_k n_k\,SEN_k}{N}=\frac{\sum_k TP_k}{N}=ACC.$$
> Tożsamość: ważona czułość = dokładność. Dobry sposób na kontrolę wyniku.

(Czułość **makro** to zwykła średnia $SEN_k$ — bez wag — i NIE równa się ACC.)

## 9.4. Problem brakującej etykiety (znając ACC)
Gdy jeden element wektora prawdziwego/predykcji jest nieznany, a dana jest dokładność:
1. Policz trafienia wśród znanych pozycji.
2. Liczba wymaganych trafień $= ACC\cdot N$.
3. Brakująca pozycja musi „dopełnić" liczbę trafień → wyznacza etykietę (zwykle = predykcja na tej pozycji, jeśli brakuje trafienia).

## 9.5. Przepis
1. Zbuduj CM (zlicz pary rzeczywista–predykcja).
2. Dla binarnego: wybierz klasę pozytywną, odczytaj TP,FN,FP,TN.
3. Policz ACC, SEN, SPEC.
4. Dla wieloklasowego: $SEN_k$ z przekątnej, potem ważona.

## Powiązane zadania
- [zdj.8 — 3 klasy, ACC=0.7, znajdź $Y$, $SEN_w$](../rozwiazania/zad_2A_zdj8_metryki_acc07.md)
- [zdj.15 — 3 klasy, ACC=0.5, znajdź $X$, $SEN_w$](../rozwiazania/zad_2A_zdj15_metryki_acc05.md)
- [zdj.13 — binarny: ACC, SEN, SPEC](../rozwiazania/zad_3_zdj13_metryki_binarne.md)
