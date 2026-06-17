# Zadanie 1B (zdjęcie 11) — Sieć „2-1-2", uczenie wagi $w_{1,2}$ i przesunięcia $b_1$

## Treść (skrót)
Sieć o strukturze 2-1-2: wejścia $p_1,p_2$; warstwa 1 — neurony 1, 2; warstwa 2 — neuron 3; warstwa 3 — neurony 4, 5 (wyjścia $a_4,a_5$). Błąd:
$$E=0.6\,e_4^2+0.4\,e_5^2,\qquad e_i=t_i-a_i,\ i=4,5.$$
Narysować architekturę, podać zbiór uczący, wyprowadzić uczenie $w_{1,2}$ i $b_1$ metodą delta (najszybszego spadku) i wstecznej propagacji.

## Architektura
```
 p1 ──┐        ┌── (1) ──┐
      ├─►(1)(2)┤         ├─►(3)──┬─►(4)─► a4
 p2 ──┘        └── (2) ──┘       └─►(5)─► a5
   warstwa 1            warstwa 2     warstwa 3
```
Sygnały:
$$n_1=w_{11}p_1+w_{12}p_2+b_1,\quad a_1=f(n_1),$$
$$n_2=w_{21}p_1+w_{22}p_2+b_2,\quad a_2=f(n_2),$$
$$n_3=w_{31}a_1+w_{32}a_2+b_3,\quad a_3=f(n_3),$$
$$n_4=w_{43}a_3+b_4,\quad a_4=f(n_4),\qquad n_5=w_{53}a_3+b_5,\quad a_5=f(n_5).$$

## Zbiór uczący
$$\big\{(\mathbf p^{(k)},\mathbf t^{(k)})\big\}_{k=1}^N,\qquad \mathbf p^{(k)}=[p_1^{(k)},p_2^{(k)}]^T,\quad \mathbf t^{(k)}=[t_4^{(k)},t_5^{(k)}]^T.$$

## Wyprowadzenie (reguła łańcuchowa wstecz)
Reguła delta: $\Delta w=-\eta\,\partial E/\partial w$.

**Warstwa 3 (wyjściowa):**
$$\frac{\partial E}{\partial a_4}=2\cdot0.6\,e_4\cdot(-1)=-1.2\,e_4,\qquad \frac{\partial E}{\partial a_5}=-0.8\,e_5.$$
Sygnały błędu (sensitivities):
$$\delta_4=\frac{\partial E}{\partial n_4}=-1.2\,e_4\,f'(n_4),\qquad \delta_5=-0.8\,e_5\,f'(n_5).$$

**Warstwa 2 (neuron 3):** neuron 3 zasila oba neurony 4 i 5:
$$\frac{\partial E}{\partial a_3}=\delta_4 w_{43}+\delta_5 w_{53},\qquad
\delta_3=\frac{\partial E}{\partial n_3}=(\delta_4 w_{43}+\delta_5 w_{53})\,f'(n_3).$$

**Warstwa 1 (neuron 1):** neuron 1 zasila neuron 3 ($\partial n_3/\partial a_1=w_{31}$):
$$\frac{\partial E}{\partial a_1}=\delta_3 w_{31},\qquad
\delta_1=\frac{\partial E}{\partial n_1}=\delta_3 w_{31}\,f'(n_1).$$

**Gradienty względem szukanych parametrów** ($n_1=w_{11}p_1+w_{12}p_2+b_1$):
$$\frac{\partial E}{\partial w_{12}}=\delta_1\,p_2,\qquad \frac{\partial E}{\partial b_1}=\delta_1.$$

## Reguły aktualizacji
$$\boxed{\,w_{12}\leftarrow w_{12}-\eta\,\delta_1\,p_2,\qquad b_1\leftarrow b_1-\eta\,\delta_1\,}$$
gdzie
$$\delta_1=f'(n_1)\,w_{31}\,f'(n_3)\big[\,w_{43}f'(n_4)(-1.2\,e_4)+w_{53}f'(n_5)(-0.8\,e_5)\,\big].$$

Rozpisane jawnie:
$$\Delta w_{12}=\eta\,p_2\,f'(n_1)\,w_{31}\,f'(n_3)\big[1.2\,e_4\,w_{43}f'(n_4)+0.8\,e_5\,w_{53}f'(n_5)\big],$$
$$\Delta b_1=\eta\,f'(n_1)\,w_{31}\,f'(n_3)\big[1.2\,e_4\,w_{43}f'(n_4)+0.8\,e_5\,w_{53}f'(n_5)\big].$$

Dla aktywacji unipolarnej (sigmoidalnej) $f'(n_i)=\alpha\,a_i(1-a_i)$.

**Interpretacja:** błąd z obu wyjść (z wagami $1.2$ i $0.8$ wynikającymi ze współczynników $0.6$ i $0.4$) propaguje się przez neuron 3 do neuronu 1; gradient $b_1$ to $\delta_1$, a gradient $w_{12}$ to $\delta_1$ przemnożone przez wejście $p_2$.
