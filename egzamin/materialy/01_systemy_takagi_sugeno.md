# 1. Rozmyte systemy ekspertowe Takagi–Sugeno (TS / TSK)

## 1.1. Idea
System Takagi–Sugeno (TS) to rozmyty system regułowy, w którym **następnik reguły jest funkcją (lub stałą) wejść**, a nie zbiorem rozmytym. Reguła:
$$R_i:\ \text{IF } x_1 \text{ is } A_1^i \text{ AND } \dots \text{ THEN } S=q_i(x).$$
- TS „zero rzędu" (singletonowy): $q_i=\text{const}$.
- TSK (1. rzędu): $q_i$ jest funkcją liniową wejść.

## 1.2. Funkcje przynależności liniowe i komplementarne
Dla zmiennej $z\in[-\alpha,\beta]$ definiujemy parę zbiorów „mały/duży":
$$N(z)=\frac{\beta-z}{\alpha+\beta},\qquad P(z)=1-N(z)=\frac{z+\alpha}{\alpha+\beta}.$$
Cechy:
- $N+P=1$ (komplementarność),
- $N$ maleje liniowo, $P$ rośnie liniowo,
- $N=1$ na lewym krańcu ($z=-\alpha$), $P=1$ na prawym ($z=\beta$).

**Przykład symetryczny** $z\in[-a,a]$: $N(z)=\dfrac{a-z}{2a}$, $P(z)=\dfrac{a+z}{2a}$.

## 1.3. Obliczanie wyjścia (średnia ważona)
Stopień dopasowania reguły = iloczyn przynależności (operator AND = iloczyn):
$$m_i=\prod_k \mu_k^i(z_k).$$
Wyjście:
$$S=\frac{\sum_i m_i q_i}{\sum_i m_i}.$$

**Kluczowy fakt (komplementarność).** Dla przynależności komplementarnych
$$\sum_i m_i=\prod_k\big(N_k+P_k\big)=1,$$
więc **mianownik znika** i wyjście to po prostu $S=\sum_i m_i q_i$.

## 1.4. Postać multiliniowa
Gdy przynależności są liniowe, $S$ jest funkcją **wieloliniową** (multilinear) wejść — wielomianem, w którym każda zmienna występuje w potędze co najwyżej 1:
$$S(z_1,\dots,z_n)=c_0+\sum_i c_i z_i+\sum_{i<j} c_{ij} z_i z_j+\dots+c_{12\dots n}z_1\cdots z_n.$$
Liczba reguł i liczba jednomianów = $2^n$.

### Wyznaczanie postaci uproszczonej (np. zadanie 1D)
1. Wypisz $S=\sum_i m_i q_i$ (mianownik = 1).
2. Podstaw $N_k,P_k$ i rozwiń.
3. Pogrupuj wyrazy → otrzymasz wielomian wieloliniowy.
4. Sprawdź w narożnikach dziedziny (tam $S$ = następnik aktywnej reguły).

## 1.5. „Generator" systemu (postać analityczna)
Definiujemy wektor bazowy (generator) wszystkich jednomianów:
$$g(z)=[\,1,\ z_1,\dots,z_n,\ z_1z_2,\dots,\ z_1z_2\cdots z_n\,]^T\quad(2^n\text{ składowych}).$$
Wówczas
$$S(z)=g^T(z)\,(\Omega^T)^{-1}\,q,$$
gdzie $q$ to wektor następników $2^n$ reguł, a $\Omega$ — macierz wartości $g$ w $2^n$ narożnikach dziedziny. To „generator" systemu PI-TS.

**Skrót praktyczny:** ponieważ $S$ jest wieloliniowa, wystarczy znać jej wartości w narożnikach (tam $N$ lub $P$ = 1). Następniki to:
$$q_{(i_1\dots i_n)}=S(\text{narożnik}),\quad \text{gdzie } i_k=0\Rightarrow z_k=-\alpha_k,\ i_k=1\Rightarrow z_k=\beta_k.$$

## 1.6. TSK odwzorowujący zadaną funkcję (np. zadanie 2B/zdj.11)
Jeśli funkcja docelowa $S(x)$ jest wieloliniowa, TSK odtwarza ją dokładnie:
1. Z dziedziny odczytaj $\alpha_k,\beta_k$ i wypisz przynależności.
2. Następniki = wartości $S$ w narożnikach.
3. (Kontrola) policz $S_{TSK}$ w punkcie środkowym i porównaj z $S$.

## 1.7. Schemat rozwiązywania zadania TS
1. Policz sygnały wejściowe (np. $z_i=\max(\dots)$).
2. Policz przynależności $N_k,P_k$.
3. Policz stopnie dopasowania $m_i$ (iloczyny); odrzuć reguły z $m_i=0$.
4. Sprawdź $\sum m_i=1$.
5. $S=\sum_i m_i q_i$ (osobno dla każdego wyjścia, np. $u_L,u_R$).

## Powiązane zadania
- [1D — uproszczona postać TS](../rozwiazania/zad_1D_takagi_sugeno.md)
- [Nawigacja robota — TS](../rozwiazania/zad_A1B1_1_nawigacja_robota.md)
- [Generator PI-TS (4 wejścia)](../rozwiazania/zad_A1B1_2_generator_PI-TS.md)
- [TSK odwzorowujący funkcję](../rozwiazania/zad_2B_zdj11_tsk.md)
