# Zadanie 2C (zdjęcie 16) — SVM: macierz Hesjanu i problem dualny (XOR, $\sigma=\sqrt2$)

## Treść (skrót)
Dane uczące (XOR symetryczny):
$$\Big(\!\begin{bmatrix}-1\\-1\end{bmatrix},-1\Big),\ \Big(\!\begin{bmatrix}-1\\1\end{bmatrix},1\Big),\ \Big(\!\begin{bmatrix}1\\-1\end{bmatrix},1\Big),\ \Big(\!\begin{bmatrix}1\\1\end{bmatrix},-1\Big).$$
Jądro $K(u,v)=\exp\!\big(-\tfrac{\lVert u-v\rVert^2}{2\sigma^2}\big)$, $\sigma=\sqrt2$ → $2\sigma^2=4$.
Wyznaczyć macierz Hesjanu i sformułować problem dualny.

## Krok 1 — wartości jądra
$K(u,v)=\exp(-\tfrac14\lVert u-v\rVert^2)$. Punkty $x_1=(-1,-1),x_2=(-1,1),x_3=(1,-1),x_4=(1,1)$.

Kwadraty odległości:

| par | $\lVert\cdot\rVert^2$ | $K=e^{-\lVert\cdot\rVert^2/4}$ |
|---|---|---|
| ten sam | 0 | $1$ |
| boki (1-2,1-3,2-4,3-4) | 4 | $e^{-1}\approx0.3679$ |
| przekątne (1-4, 2-3) | 8 | $e^{-2}\approx0.1353$ |

Macierz jądra:
$$K=\begin{bmatrix}
1 & 0.3679 & 0.3679 & 0.1353\\
0.3679 & 1 & 0.1353 & 0.3679\\
0.3679 & 0.1353 & 1 & 0.3679\\
0.1353 & 0.3679 & 0.3679 & 1
\end{bmatrix}.$$

## Krok 2 — macierz Hesjanu $H_{ij}=y_iy_jK(x_i,x_j)$
$y=[-1,+1,+1,-1]$ (ten sam wzorzec znaków co w zad. 1/zdj.13):
$$\boxed{\,H=\begin{bmatrix}
1 & -0.3679 & -0.3679 & 0.1353\\
-0.3679 & 1 & 0.1353 & -0.3679\\
-0.3679 & 0.1353 & 1 & -0.3679\\
0.1353 & -0.3679 & -0.3679 & 1
\end{bmatrix}\,}$$

## Krok 3 — problem dualny (miękki margines)
$$\max_{\boldsymbol\alpha}\ W(\boldsymbol\alpha)=\sum_{i=1}^4\alpha_i-\tfrac12\boldsymbol\alpha^TH\boldsymbol\alpha$$
przy ograniczeniach:
$$\sum_{i=1}^4 y_i\alpha_i=0\ \Longleftrightarrow\ -\alpha_1+\alpha_2+\alpha_3-\alpha_4=0,\qquad 0\le\alpha_i\le C.$$

Równoważnie (minimalizacja):
$$\min_{\boldsymbol\alpha}\ \tfrac12\boldsymbol\alpha^TH\boldsymbol\alpha-\mathbf1^T\boldsymbol\alpha,\quad \text{s.t. } \mathbf y^T\boldsymbol\alpha=0,\ 0\le\alpha_i\le C.$$

Jest to zadanie QP z macierzą Hesjanu $H$ (symetryczna, dodatnio półokreślona dzięki własności jądra Mercera), jednym ograniczeniem równościowym i ograniczeniami pudełkowymi. Jądro Gaussa umożliwia separację nieliniowo separowalnego zbioru XOR.
