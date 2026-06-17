# 7. k-means, kNN, PNN

## 7.1. k-średnich (k-means) — grupowanie bez nadzoru
**Cel:** podział punktów na $k$ klastrów minimalizujący sumę kwadratów odległości do centrów.

**Algorytm (Lloyd):**
1. Inicjalizuj $k$ centrów $c_1,\dots,c_k$.
2. **Przypisanie:** każdy punkt → najbliższe centrum (odległość euklidesowa; wystarczy $d^2$).
3. **Aktualizacja:** centrum = średnia punktów w klastrze.
4. Powtarzaj 2–3 aż przypisania się nie zmieniają (zbieżność).

**Wskazówki:**
- Liczenie $d^2$ (bez pierwiastka) wystarcza do porównań.
- Zapisz każdą iterację: tabela odległości → przypisania → nowe centra.
- Zatrzymanie: gdy w kolejnej iteracji przypisania są identyczne.

→ [Zadanie 2F (k-means)](../rozwiazania/zad_2F_kmeans.md)

## 7.2. kNN — k najbliższych sąsiadów (klasyfikacja z nadzorem)
**Algorytm:**
1. Policz odległości punktu testowego $P$ do wszystkich punktów uczących.
2. Wybierz $k$ najbliższych.
3. Głosowanie większościowe klas wśród sąsiadów → klasa $P$.

**Wskazówki:**
- Przy remisach odległości włącz wszystkie punkty o tej samej (najmniejszej kolejnej) odległości.
- Dla $k=3$ wystarczy posortować odległości i wziąć trzy pierwsze.
- Brak fazy uczenia (lazy learning) — cała praca przy predykcji.

→ [Zadanie 1E (kNN)](../rozwiazania/zad_1E_knn.md)

## 7.3. PNN — sieć neuronowa probabilistyczna
Estymator gęstości Parzena zamieniony w klasyfikator. **Architektura 4-warstwowa:**
1. **Wejściowa** — podaje $x$ do wszystkich neuronów.
2. **Wzorcowa** — po jednym neuronie na wzorzec; neuron $i$ liczy jądro
   $$K(x,x_i)=\exp\!\Big(-\frac{\lVert x-x_i\rVert^2}{2\sigma_i^2}\Big).$$
3. **Sumacyjna** — po jednym neuronie na klasę; uśrednia (lub sumuje) jądra:
   $$g_k(x)=\frac1{n_k}\sum_{i\in C_k}K(x,x_i).$$
4. **Decyzyjna** — $\text{class}(x)=\arg\max_k g_k(x)$.

**Wskazówki:**
- Uprość jądro: dla $\sigma=1/\sqrt2$ jest $2\sigma^2=1$, więc $K=e^{-\lVert x-x_i\rVert^2}$.
- Pamiętaj o dzieleniu przez liczność klasy $n_k$ (średnia, nie suma).
- Dominują wzorce najbliższe $x$ (jądro szybko maleje).

→ [Zadanie 2E (PNN)](../rozwiazania/zad_2E_pnn.md)

## 7.4. Porównanie
| metoda | nadzór | faza uczenia | działanie |
|---|---|---|---|
| k-means | nie | iteracyjne | grupowanie |
| kNN | tak | brak | głosowanie sąsiadów |
| PNN | tak | zapamiętanie wzorców | suma jąder Gaussa per klasa |
