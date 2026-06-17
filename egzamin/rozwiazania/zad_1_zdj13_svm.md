# Zadanie 1 (zdjęcie 13) — SVM: macierz Hessego i problem dualny (XOR, jądro Gaussa)

## Treść (skrót)
Dane uczące (nieliniowo separowalne — XOR):
$$\Big(\!\begin{bmatrix}0\\0\end{bmatrix},-1\Big),\ \Big(\!\begin{bmatrix}0\\1\end{bmatrix},+1\Big),\ \Big(\!\begin{bmatrix}1\\0\end{bmatrix},+1\Big),\ \Big(\!\begin{bmatrix}1\\1\end{bmatrix},-1\Big).$$
Jądro Gaussa $K^\*(u,v)=\exp\!\big(-\tfrac{(u-v)^T(u-v)}{2\sigma^2}\big)$, $\sigma=\tfrac1{\sqrt3}$ → $2\sigma^2=\tfrac23$.
**Tylko sformułować** macierz Hessego i problem dualny (bez rozwiązywania).

## Krok 1 — wartości jądra
$2\sigma^2=2/3$, więc $K(u,v)=\exp(-\tfrac32\lVert u-v\rVert^2)$.

Kwadraty odległości między punktami $x_1=(0,0),x_2=(0,1),x_3=(1,0),x_4=(1,1)$:

| par | $\lVert\cdot\rVert^2$ | $K=e^{-1.5\,\lVert\cdot\rVert^2}$ |
|---|---|---|
| ten sam | 0 | $1$ |
| sąsiednie (np. 1-2,1-3,2-4,3-4) | 1 | $e^{-1.5}\approx0.2231$ |
| przekątne (1-4, 2-3) | 2 | $e^{-3}\approx0.0498$ |

Macierz jądra:
$$K=\begin{bmatrix}
1 & 0.2231 & 0.2231 & 0.0498\\
0.2231 & 1 & 0.0498 & 0.2231\\
0.2231 & 0.0498 & 1 & 0.2231\\
0.0498 & 0.2231 & 0.2231 & 1
\end{bmatrix}.$$

## Krok 2 — macierz Hessego $H_{ij}=y_i y_j K(x_i,x_j)$
$y=[-1,+1,+1,-1]$, więc znaki: $y_iy_j$ daje $-$ dla par o przeciwnych etykietach.
$$\boxed{\,H=\begin{bmatrix}
1 & -0.2231 & -0.2231 & 0.0498\\
-0.2231 & 1 & 0.0498 & -0.2231\\
-0.2231 & 0.0498 & 1 & -0.2231\\
0.0498 & -0.2231 & -0.2231 & 1
\end{bmatrix}\,}$$

## Krok 3 — sformułowanie problemu dualnego (miękki margines, dane nieseparowalne)
$$\max_{\boldsymbol\alpha}\ W(\boldsymbol\alpha)=\sum_{i=1}^4\alpha_i-\frac12\sum_{i=1}^4\sum_{j=1}^4\alpha_i\alpha_j\,y_iy_j\,K(x_i,x_j)
=\mathbf 1^T\boldsymbol\alpha-\tfrac12\boldsymbol\alpha^T H\boldsymbol\alpha$$
przy ograniczeniach:
$$\sum_{i=1}^4 y_i\alpha_i=0\ \Longleftrightarrow\ -\alpha_1+\alpha_2+\alpha_3-\alpha_4=0,$$
$$0\le\alpha_i\le C,\quad i=1,\dots,4.$$

To jest zadanie programowania kwadratowego (QP) z funkcją celu wypukłą po $-\tfrac12\boldsymbol\alpha^TH\boldsymbol\alpha$ (minimalizacja $\tfrac12\boldsymbol\alpha^TH\boldsymbol\alpha-\mathbf1^T\boldsymbol\alpha$), z jednym ograniczeniem równościowym i ograniczeniami pudełkowymi $[0,C]$.

> Zgodnie z poleceniem problem został **tylko sformułowany**. Jądro Gaussa pozwala rozdzielić nieseparowalny liniowo zbiór XOR w przestrzeni cech.
