# Zadanie 2D — ADALINE (uczenie Widrowa–Hoffa)

## Treść (skrót)
Neuron liniowy ADALINE o jednym wejściu i jednym wyjściu, uczony minimalizacją
$$E=\sum_{k=1}^4 (d_k-y_k)^2.$$
Dane uczące: $\{(a,d_1),(-a,d_2),(b,d_3),(-b,d_4)\}$. Stosujemy rozszerzone wektory wag i wejść. Wzór:
$$w^\*=[w^\*,b^\*]^T=(XX^T)^{-1}XD.$$

## Rozwiązanie
Dla neuronu $y=w\,x+b$ rozszerzamy wejście o stałą 1, więc kolumny macierzy $X$ to $[x_k,1]^T$:
$$X=\begin{bmatrix} a & -a & b & -b\\ 1 & 1 & 1 & 1\end{bmatrix},\qquad
D=\begin{bmatrix} d_1\\ d_2\\ d_3\\ d_4\end{bmatrix}.$$

**Macierz korelacji:**
$$XX^T=\begin{bmatrix} a^2+a^2+b^2+b^2 & a-a+b-b\\ a-a+b-b & 1+1+1+1\end{bmatrix}
=\begin{bmatrix} 2(a^2+b^2) & 0\\ 0 & 4\end{bmatrix}.$$

Macierz jest diagonalna, więc odwrotność jest prosta:
$$(XX^T)^{-1}=\begin{bmatrix} \dfrac{1}{2(a^2+b^2)} & 0\\[2mm] 0 & \dfrac14\end{bmatrix}.$$

**Wektor korelacji wejście–cel:**
$$XD=\begin{bmatrix} a d_1 - a d_2 + b d_3 - b d_4\\ d_1+d_2+d_3+d_4\end{bmatrix}
=\begin{bmatrix} a(d_1-d_2)+b(d_3-d_4)\\ d_1+d_2+d_3+d_4\end{bmatrix}.$$

**Rozwiązanie optymalne:**
$$\boxed{\,w^\*=\frac{a(d_1-d_2)+b(d_3-d_4)}{2(a^2+b^2)},\qquad
b^\*=\frac{d_1+d_2+d_3+d_4}{4}\,}$$

## Interpretacja
- Przesunięcie $b^\*$ jest po prostu **średnią wartości pożądanych** — neuron centruje wyjście wokół średniej.
- Waga $w^\*$ jest znormalizowaną kowariancją wejście–cel; mianownik $2(a^2+b^2)$ to energia (wariancja nieunormowana) sygnału wejściowego.
- Diagonalność $XX^T$ wynika z symetrii zbioru wejść ($\sum x_k=0$), co rozprzęga estymację wagi i przesunięcia.
