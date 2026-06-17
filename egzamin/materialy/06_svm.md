# 6. SVM — maszyna wektorów wspierających

## 6.1. Problem pierwotny (margines miękki)
Dla danych $\{(x_i,y_i)\}$, $y_i\in\{-1,+1\}$:
$$\min_{w,b,\xi}\ \tfrac12\lVert w\rVert^2 + C\sum_i \xi_i,\qquad \text{s.t. } y_i(w^T\phi(x_i)+b)\ge 1-\xi_i,\ \xi_i\ge0.$$
$C$ — kara za błędy (dane nieseparowalne wymagają $\xi_i$ i skończonego $C$).

## 6.2. Problem dualny
$$\max_{\boldsymbol\alpha}\ W(\boldsymbol\alpha)=\sum_i\alpha_i-\tfrac12\sum_{i,j}\alpha_i\alpha_j\,y_iy_j\,K(x_i,x_j)$$
przy ograniczeniach:
$$\sum_i y_i\alpha_i=0,\qquad 0\le\alpha_i\le C.$$
W zapisie macierzowym ($\mathbf1$ — wektor jedynek):
$$\max_{\boldsymbol\alpha}\ \mathbf1^T\boldsymbol\alpha-\tfrac12\boldsymbol\alpha^T H\boldsymbol\alpha,\quad \text{s.t. } \mathbf y^T\boldsymbol\alpha=0,\ 0\le\boldsymbol\alpha\le C.$$

## 6.3. Macierz Hessego
$$\boxed{\,H_{ij}=y_i\,y_j\,K(x_i,x_j)\,}$$
- Symetryczna, dodatnio półokreślona (dla jąder Mercera).
- To Hesjan funkcji celu (z dokładnością do znaku w sformułowaniu min/max).

## 6.4. Funkcje jądra (kernel trick)
Jądro Gaussa (RBF):
$$K(u,v)=\exp\!\Big(-\frac{\lVert u-v\rVert^2}{2\sigma^2}\Big).$$
- Pozwala separować dane nieliniowo separowalne (np. XOR) bez jawnego mapowania $\phi$.
- Uwaga na parametr: $\sigma=\tfrac1{\sqrt3}\Rightarrow 2\sigma^2=\tfrac23$; $\sigma=\sqrt2\Rightarrow 2\sigma^2=4$.

## 6.5. Przepis „wyznacz $H$ i sformułuj dualny"
1. Policz wszystkie odległości$^2$ między punktami.
2. Policz $K(x_i,x_j)=\exp(-\lVert\cdot\rVert^2/2\sigma^2)$ (macierz jądra).
3. Pomnóż przez znaki $y_iy_j$ → macierz $H$.
4. Zapisz funkcję celu $\mathbf1^T\alpha-\tfrac12\alpha^TH\alpha$ i ograniczenia $\mathbf y^T\alpha=0$, $0\le\alpha_i\le C$.

> Jeśli polecenie mówi „tylko sformułować" — nie rozwiązuj QP, podaj $H$ i ograniczenia.

## 6.6. Funkcja decyzyjna
$$f(x)=\text{sgn}\Big(\sum_i \alpha_i y_i K(x_i,x)+b\Big).$$
Wektory wspierające to te $x_i$, dla których $\alpha_i>0$.

## Powiązane zadania
- [zdj.13 — $H$ i dual, $\sigma=1/\sqrt3$](../rozwiazania/zad_1_zdj13_svm.md)
- [zdj.16 (2C) — $H$ i dual, $\sigma=\sqrt2$](../rozwiazania/zad_2C_zdj16_svm.md)
