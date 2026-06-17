# 3. Sieci neuronowe progowe i funkcje boolowskie

## 3.1. Neuron progowy (perceptron)
$$n=\sum_j w_j p_j + b,\qquad a=f(n),\qquad f(x)=\begin{cases}0,&x<0\\ 1,&x\ge0\end{cases}.$$
Pojedynczy neuron realizuje **półpłaszczyznę** decyzyjną: $a=1\iff \sum_j w_j p_j\ge -b$.

Notacja zadań: $w_{ij}$ — waga neuronu $i$ od wejścia $j$; $b_j$ — przesunięcie (bias) neuronu $j$.

## 3.2. Odczytywanie funkcji logicznej z wag — metoda
1. **Wypisz $n_i$ każdego neuronu** warstwy 1 jako kombinację wejść.
2. **Szukaj neuronów stale aktywnych/wyłączonych** — bardzo upraszcza analizę.
   - Jeśli $n_i<0$ dla wszystkich wejść binarnych → $a_i=0$ zawsze.
   - Jeśli $n_i\ge0$ zawsze → $a_i=1$.
3. **Zbuduj tabelę prawdy** warstwy 1 dla wszystkich kombinacji wejść ($2^k$ wierszy).
4. **Policz warstwę wyjściową** na podstawie $a_1,a_2,\dots$
5. **Rozpoznaj bramkę** wyjścia. Typowe wzorce dla 2 wejść:
   - AND: waga $1,1$, bias $-1.5$ (potrzeba obu).
   - OR: waga $1,1$, bias $-0.5$ (wystarczy jedno).
   - NOT: waga $-1$, bias $0.5$.
6. **Zapisz funkcję** w postaci sumy minteremów / uprość (Karnaugh).

## 3.3. Przykładowe wnioski z zadań
- Neuron z dużą ujemną stałą (np. $b=-3$) i ujemnymi wagami często jest **stale wyłączony** → upraszcza sieć.
- Neuron wyjściowy typu AND zapala się tylko gdy wszystkie potrzebne neurony ukryte = 1.
- Często wyjście sprowadza się do jednego neuronu ukrytego ($a_3=a_1$), bo drugi jest martwy.

## 3.4. Interpretacja geometryczna
- Warstwa 1: zbiór prostych (hiperpłaszczyzn) dzielących przestrzeń wejść.
- Warstwa 2: logiczna kombinacja (AND/OR) tych półpłaszczyzn → obszary decyzyjne (także niewypukłe, np. XOR wymaga 2 warstw).

## Powiązane zadania
- [2B (zdj.3) — wynik: OR](../rozwiazania/zad_2B_siec_boolowska.md)
- [zdj.12 — 3 wejścia, wynik: $(\lnot b\wedge(a\vee c))\vee(a\wedge b\wedge c)$](../rozwiazania/zad_zdj12_siec_boolowska_3wej.md)
- [zdj.19 — wynik: $a\vee\lnot b$ (implikacja)](../rozwiazania/zad_2A_zdj19_siec_boolowska.md)
