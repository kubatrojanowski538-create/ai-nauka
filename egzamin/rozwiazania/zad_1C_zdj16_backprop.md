# Zadanie 1C (zdjęcie 16) — Uczenie wagi $w_{3,1}$ i przesunięcia $b_3$ (backprop)

## Treść (skrót)
Dwuwarstwowa sieć: wejścia $p_1,p_2$; warstwa 1 — neurony 1, 2, 3; warstwa 2 — neurony 4, 5 (wyjścia $a_4,a_5$). Błąd:
$$E=0.4\,e_4^2+0.6\,e_5^2,\qquad e_4=t_4-a_4,\ e_5=t_5-a_5.$$
Podać zbiór uczący i wyprowadzić uczenie $w_{3,1}$ i $b_3$ metodą delta wstecznej propagacji.

## Sygnały sieci
Warstwa 1 ($j=1,2,3$): $n_j=w_{j1}p_1+w_{j2}p_2+b_j$, $a_j=f(n_j)$.
Warstwa 2:
$$n_4=w_{41}a_1+w_{42}a_2+w_{43}a_3+b_4,\ a_4=f(n_4),$$
$$n_5=w_{51}a_1+w_{52}a_2+w_{53}a_3+b_5,\ a_5=f(n_5).$$

## Zbiór uczący
$$\big\{(\mathbf p^{(k)},\mathbf t^{(k)})\big\}_{k=1}^N,\qquad \mathbf p^{(k)}=[p_1^{(k)},p_2^{(k)}]^T,\quad \mathbf t^{(k)}=[t_4^{(k)},t_5^{(k)}]^T.$$

## Wyprowadzenie
Szukamy $w_{31}$ (waga neuronu 3 od wejścia $p_1$) oraz $b_3$ (przesunięcie neuronu 3). Neuron 3 leży w warstwie ukrytej i zasila **oba** neurony wyjściowe 4 i 5.

**Warstwa wyjściowa:**
$$\frac{\partial E}{\partial a_4}=-0.8\,e_4,\qquad \frac{\partial E}{\partial a_5}=-1.2\,e_5,$$
$$\delta_4=\frac{\partial E}{\partial n_4}=-0.8\,e_4\,f'(n_4),\qquad \delta_5=-1.2\,e_5\,f'(n_5).$$

**Neuron 3 (ukryty):** $\partial n_4/\partial a_3=w_{43}$, $\partial n_5/\partial a_3=w_{53}$, więc
$$\frac{\partial E}{\partial a_3}=\delta_4 w_{43}+\delta_5 w_{53},\qquad
\delta_3=\frac{\partial E}{\partial n_3}=(\delta_4 w_{43}+\delta_5 w_{53})\,f'(n_3).$$

**Gradienty** ($n_3=w_{31}p_1+w_{32}p_2+b_3$):
$$\frac{\partial E}{\partial w_{31}}=\delta_3\,p_1,\qquad \frac{\partial E}{\partial b_3}=\delta_3.$$

## Reguły aktualizacji
$$\boxed{\,w_{31}\leftarrow w_{31}-\eta\,\delta_3\,p_1,\qquad b_3\leftarrow b_3-\eta\,\delta_3\,}$$
gdzie
$$\delta_3=f'(n_3)\big[w_{43}f'(n_4)(-0.8\,e_4)+w_{53}f'(n_5)(-1.2\,e_5)\big].$$

Jawnie:
$$\Delta w_{31}=\eta\,p_1\,f'(n_3)\big[0.8\,e_4\,w_{43}f'(n_4)+1.2\,e_5\,w_{53}f'(n_5)\big],$$
$$\Delta b_3=\eta\,f'(n_3)\big[0.8\,e_4\,w_{43}f'(n_4)+1.2\,e_5\,w_{53}f'(n_5)\big].$$

Dla aktywacji unipolarnej $f'(n_i)=\alpha\,a_i(1-a_i)$.

**Komentarz:** neuron 3 jest tylko o jeden poziom od wyjścia, więc jego sygnał błędu $\delta_3$ zbiera wkłady obu wyjść ważone $w_{43},w_{53}$ i współczynnikami $0.8,1.2$ (z $0.4,0.6$ w funkcji błędu). Gradient $b_3=\delta_3$, a $w_{31}=\delta_3\cdot p_1$.
