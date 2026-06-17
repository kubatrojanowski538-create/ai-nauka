# 5. Wsteczna propagacja błędów (reguła delta najszybszego spadku)

## 5.1. Idea
Uczenie sieci wielowarstwowej polega na minimalizacji błędu $E$ metodą gradientową:
$$w\leftarrow w-\eta\,\frac{\partial E}{\partial w}.$$
Gradienty liczymy **regułą łańcuchową od wyjścia w stronę wejścia** (stąd „wsteczna propagacja").

## 5.2. Oznaczenia
Dla neuronu $i$: pobudzenie $n_i=\sum_j w_{ij}a_j+b_i$, wyjście $a_i=f(n_i)$.
**Sygnał błędu** (sensitivity):
$$\delta_i=\frac{\partial E}{\partial n_i}.$$
Wtedy zawsze:
$$\frac{\partial E}{\partial w_{ij}}=\delta_i\,a_j,\qquad \frac{\partial E}{\partial b_i}=\delta_i.$$
Czyli: **gradient wagi = sygnał błędu neuronu × wejście do tej wagi**, a gradient biasu = sam sygnał błędu.

## 5.3. Reguły obliczania $\delta$
**Neuron wyjściowy** (np. $E=\sum_m c_m(t_m-a_m)^2$):
$$\frac{\partial E}{\partial a_m}=-2c_m(t_m-a_m)=-2c_m e_m,\qquad \delta_m=\frac{\partial E}{\partial a_m}\,f'(n_m).$$

**Neuron ukryty** $i$, który zasila zbiór neuronów $\{m\}$ następnej warstwy:
$$\delta_i=\Big(\sum_m \delta_m\,w_{mi}\Big)\,f'(n_i).$$

## 5.4. Pochodne funkcji aktywacji
- Sigmoida unipolarna $f(n)=\dfrac1{1+e^{-\alpha n}}$: $\quad f'(n)=\alpha\,a(1-a)$.
- Tangens (bipolarna) $f(n)=\tanh$: $\quad f'=\alpha(1-a^2)$ (zależnie od konwencji).

## 5.5. Przepis na „wyprowadź uczenie wagi $w_{ij}$"
1. Wypisz wszystkie sygnały sieci ($n,a$ warstwa po warstwie).
2. Policz $\delta$ neuronów wyjściowych (uwzględnij wagi $c_m$ w funkcji błędu).
3. Propaguj $\delta$ wstecz aż do neuronu $i$ (sumuj po wszystkich ścieżkach do wyjść!).
4. Zapisz $\dfrac{\partial E}{\partial w_{ij}}=\delta_i a_j$ oraz $\dfrac{\partial E}{\partial b_i}=\delta_i$.
5. Reguła: $w_{ij}\leftarrow w_{ij}-\eta\,\delta_i a_j$, $b_i\leftarrow b_i-\eta\,\delta_i$.

> Jeśli neuron ukryty zasila kilka wyjść (np. pojedynczy neuron warstwy środkowej), jego $\delta$ jest **sumą** wkładów od wszystkich wyjść.

## 5.6. Wpływ wag w funkcji błędu
Dla $E=c_4 e_4^2+c_5 e_5^2$ sygnały wyjściowe niosą czynniki $2c_4,2c_5$. Np. $E=0.6e_4^2+0.4e_5^2\Rightarrow$ czynniki $1.2$ i $0.8$; $E=\tfrac14e_4^2+\tfrac34e_5^2\Rightarrow \tfrac12$ i $\tfrac32$.

## Powiązane zadania
- [zdj.11 — uczenie $w_{1,2}, b_1$ (sieć 2-1-2)](../rozwiazania/zad_1B_zdj11_siec_2-1-2.md)
- [zdj.13 — uczenie $w_{1,2}$ (sigmoida)](../rozwiazania/zad_2_zdj13_backprop.md)
- [zdj.16 — uczenie $w_{3,1}, b_3$](../rozwiazania/zad_1C_zdj16_backprop.md)
