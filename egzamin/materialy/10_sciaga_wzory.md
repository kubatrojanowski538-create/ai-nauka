# 10. Ściąga wzorów (skrót)

## Operatory Łukasiewicza / ograniczone
- implikacja: $a\to b=\min(1,1-a+b)$
- OR: $a\oplus b=\min(1,a+b)$
- AND / łączenie reguł: $a\otimes b=\max(0,a+b-1)$
- negacja: $\lnot a=1-a$;  min/max gdy zaznaczono

## Uogólniony system ekspertowy (4 kroki)
$$R_k(x,y)=A_k(x)\to Q_k(y),\quad R=\bigotimes_k R_k,$$
$$B'(y)=\sup_x[A'(x)\otimes R(x,y)],\quad y^\*=\frac{\sum_j y_j B'(y_j)}{\sum_j B'(y_j)}.$$

## Takagi–Sugeno
- przynależności: $N=\frac{\beta-z}{\alpha+\beta}$, $P=1-N$; $N+P=1$
- wyjście: $S=\frac{\sum m_i q_i}{\sum m_i}$, a przy komplementarności $\sum m_i=1\Rightarrow S=\sum m_i q_i$
- następniki TSK: wartości $S$ w narożnikach dziedziny
- generator: $S(z)=g^T(z)(\Omega^T)^{-1}q$, $g=[1,z_1,\dots,z_1z_2\cdots z_n]^T$

## Neuron progowy
$$a=f\Big(\sum_j w_j p_j+b\Big),\quad f(x)=[x\ge0].$$
AND: wagi $1,1$, bias $-1.5$;  OR: $-0.5$;  NOT: waga $-1$, bias $0.5$.

## ADALINE (Widrow–Hoff)
$$w^\*=(XX^T)^{-1}XD,\qquad X=\begin{bmatrix}x_1&\cdots&x_P\\1&\cdots&1\end{bmatrix}.$$
Symetryczne wejścia: $b^\*=\overline d$, $w^\*=\frac{\sum x_k d_k}{\sum x_k^2}$.

## Wsteczna propagacja (delta)
$$\frac{\partial E}{\partial w_{ij}}=\delta_i a_j,\quad \frac{\partial E}{\partial b_i}=\delta_i,\quad w\leftarrow w-\eta\frac{\partial E}{\partial w}.$$
- wyjściowy: $\delta_m=\frac{\partial E}{\partial a_m}f'(n_m)$, gdzie $E=\sum c_m e_m^2\Rightarrow \frac{\partial E}{\partial a_m}=-2c_m e_m$
- ukryty: $\delta_i=(\sum_m \delta_m w_{mi})f'(n_i)$
- sigmoida: $f'=\alpha\,a(1-a)$

## SVM
$$\max_\alpha\ \mathbf1^T\alpha-\tfrac12\alpha^TH\alpha,\quad \mathbf y^T\alpha=0,\ 0\le\alpha_i\le C,$$
$$H_{ij}=y_iy_jK(x_i,x_j),\quad K(u,v)=e^{-\lVert u-v\rVert^2/2\sigma^2}.$$

## k-means / kNN / PNN
- k-means: przypisz do najbliższego centrum → przelicz centra (średnia) → powtórz do zbieżności.
- kNN: $k$ najbliższych → głosowanie większościowe.
- PNN: $g_k(x)=\frac1{n_k}\sum_{i\in C_k}e^{-\lVert x-x_i\rVert^2/2\sigma^2}$, $\text{class}=\arg\max_k g_k$.

## GEP
- dekoduj K-wyrażenie wszerz (arność: AND/OR=2, NOT=1), połącz geny.
- fitness = dokładność = zgodne wiersze / $2^n$.

## Metryki klasyfikatora
$$ACC=\frac{TP+TN}{N},\quad SEN=\frac{TP}{TP+FN},\quad SPEC=\frac{TN}{TN+FP},$$
$$SEN_{\text{ważona}}=ACC.$$
