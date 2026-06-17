# 4. ADALINE i reguła Widrowa–Hoffa (LMS)

## 4.1. Model
ADALINE = neuron **liniowy** (bez progu na wyjściu uczenia): $y=w^T x + b$. Dla pojedynczego wejścia $y=wx+b$.

## 4.2. Kryterium
Minimalizujemy błąd średniokwadratowy na zbiorze uczącym:
$$E=\sum_{k=1}^P (d_k-y_k)^2.$$

## 4.3. Rozwiązanie normalne (batch)
Stosujemy **wektory rozszerzone**: do każdego wejścia dopisujemy stałą 1, aby objąć bias.
Macierz wejść (kolumny = przykłady):
$$X=\begin{bmatrix} x_1 & x_2 & \cdots & x_P\\ 1 & 1 & \cdots & 1\end{bmatrix},\qquad D=[d_1,\dots,d_P]^T.$$
Rozwiązanie minimalizujące $E$ (równania normalne):
$$\boxed{\,w^\*=\begin{bmatrix}w^\*\\ b^\*\end{bmatrix}=(XX^T)^{-1}XD\,}$$

- $XX^T$ — macierz autokorelacji wejść (wymiar $(n{+}1)\times(n{+}1)$),
- $XD$ — wektor korelacji wejście–cel.

## 4.4. Wskazówki rachunkowe
- Jeśli wejścia są **symetryczne** ($\sum_k x_k=0$), to $XX^T$ jest **diagonalna** → odwracanie trywialne, a estymacje wagi i biasu się rozprzęgają.
- Wtedy zwykle:
  $$b^\*=\frac1P\sum_k d_k\ (\text{średnia celów}),\qquad w^\*=\frac{\sum_k x_k d_k}{\sum_k x_k^2}.$$

## 4.5. Wariant iteracyjny (reguła delta Widrowa–Hoffa)
$$w\leftarrow w+\eta\,(d_k-y_k)\,x_k.$$
Rozwiązanie normalne to punkt zbieżności tej reguły dla małego $\eta$.

## Powiązane zadania
- [2D — ADALINE, rozwiązanie $(XX^T)^{-1}XD$](../rozwiazania/zad_2D_adaline.md)
