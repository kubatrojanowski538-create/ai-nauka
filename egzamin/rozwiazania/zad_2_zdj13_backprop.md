# Zadanie 2 (zdjęcie 13) — Wsteczna propagacja: uczenie wagi $w_{1,2}$

## Treść (skrót)
Trójwarstwowa sieć: wejścia $p_1,p_2$; warstwa 1 — neurony 1, 2; warstwa 2 — neuron 3; warstwa 3 — neurony 4, 5 (wyjścia $a_4,a_5$). Cel:
$$E=\tfrac14(t_4-a_4)^2+\tfrac34(t_5-a_5)^2.$$
Aktywacje unipolarne identyczne $f_i(n_i)=y_i=\dfrac1{1+e^{-\alpha n_i}}$, z $f_i'(n_i)=\alpha\,y_i(1-y_i)$.
Wyprowadzić uczenie $w_{1,2}$ metodą delta najszybszego spadku i wstecznej propagacji.

## Sygnały sieci
$$n_1=w_{11}p_1+w_{12}p_2+b_1,\ a_1=f(n_1);\qquad n_2=w_{21}p_1+w_{22}p_2+b_2,\ a_2=f(n_2);$$
$$n_3=w_{31}a_1+w_{32}a_2+b_3,\ a_3=f(n_3);$$
$$n_4=w_{43}a_3+b_4,\ a_4=f(n_4);\qquad n_5=w_{53}a_3+b_5,\ a_5=f(n_5).$$

## Wyprowadzenie (reguła łańcuchowa wstecz)
Oznaczmy $e_4=t_4-a_4$, $e_5=t_5-a_5$.

**Warstwa wyjściowa:**
$$\frac{\partial E}{\partial a_4}=2\cdot\tfrac14 e_4(-1)=-\tfrac12 e_4,\qquad
\frac{\partial E}{\partial a_5}=2\cdot\tfrac34 e_5(-1)=-\tfrac32 e_5.$$
$$\delta_4=\frac{\partial E}{\partial n_4}=-\tfrac12 e_4\,\alpha a_4(1-a_4),\qquad
\delta_5=-\tfrac32 e_5\,\alpha a_5(1-a_5).$$

**Neuron 3 (zasila 4 i 5):**
$$\delta_3=\frac{\partial E}{\partial n_3}=(\delta_4 w_{43}+\delta_5 w_{53})\,\alpha a_3(1-a_3).$$

**Neuron 1 (zasila 3):**
$$\delta_1=\frac{\partial E}{\partial n_1}=\delta_3 w_{31}\,\alpha a_1(1-a_1).$$

**Gradient względem $w_{12}$** ($n_1=w_{11}p_1+w_{12}p_2+b_1$):
$$\frac{\partial E}{\partial w_{12}}=\delta_1\,p_2.$$

## Reguła aktualizacji
$$\boxed{\,w_{12}\leftarrow w_{12}-\eta\,\delta_1\,p_2\,}$$
gdzie po podstawieniu:
$$\delta_1=\alpha a_1(1-a_1)\,w_{31}\,\alpha a_3(1-a_3)\Big[w_{43}\,\alpha a_4(1-a_4)\big(-\tfrac12 e_4\big)+w_{53}\,\alpha a_5(1-a_5)\big(-\tfrac32 e_5\big)\Big].$$

Postać jawna przyrostu:
$$\Delta w_{12}=\eta\,p_2\,\alpha^3 a_1(1-a_1)\,w_{31}\,a_3(1-a_3)\Big[\tfrac12 e_4 w_{43}a_4(1-a_4)+\tfrac32 e_5 w_{53}a_5(1-a_5)\Big].$$

**Komentarz:** wyjście $a_5$ wnosi 3-krotnie większy wkład niż $a_4$ (wagi $\tfrac34$ vs $\tfrac14$ w funkcji błędu), co widać w czynnikach $\tfrac12$ i $\tfrac32$. Każda warstwa wstecz dokłada czynnik $\alpha\,a(1-a)$ (pochodna sigmoidy) oraz odpowiednią wagę połączenia.
