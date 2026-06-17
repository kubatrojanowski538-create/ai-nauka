# Materiały do nauki — Inteligencja obliczeniowa / Systemy ekspertowe i sieci neuronowe

Zakres materiału odpowiada zadaniom z pliku `zadania_odczytane.pdf`. Każdy plik omawia jedną grupę zagadnień: teoria, wzory i metoda rozwiązywania krok po kroku.

## Spis treści

1. [Rozmyte systemy ekspertowe Takagi–Sugeno (TS / TSK)](01_systemy_takagi_sugeno.md)
   — przynależności liniowe komplementarne, średnia ważona, postać multiliniowa, generator, system PI-TS.
2. [Uogólnione (relacyjne) systemy ekspertowe](02_uogolnione_systemy_ekspertowe.md)
   — operatory Łukasiewicza, relacje rozmyte, wnioskowanie sup-⊗, wyostrzanie.
3. [Sieci neuronowe — perceptron progowy i funkcje boolowskie](03_sieci_boolowskie_progowe.md)
   — funkcja skokowa, odczytywanie funkcji logicznej z wag.
4. [ADALINE i reguła Widrowa–Hoffa](04_adaline_widrow_hoff.md)
   — minimalizacja MSE, rozwiązanie normalne $(XX^T)^{-1}XD$.
5. [Wsteczna propagacja błędów (reguła delta)](05_backpropagation_delta.md)
   — gradienty, sygnały błędu $\delta$, aktualizacja wag dowolnej warstwy.
6. [SVM — maszyna wektorów wspierających](06_svm.md)
   — margines, jądra, macierz Hessego, problem dualny.
7. [Metody uczenia bez nadzoru i z nadzorem: k-means, kNN, PNN](07_kmeans_knn_pnn.md)
8. [Algorytm GEP (Gene Expression Programming)](08_gep.md)
   — dekodowanie K-wyrażeń, funkcja dopasowania.
9. [Ocena klasyfikatorów — macierz pomyłek i metryki](09_metryki_klasyfikatorow.md)
   — ACC, SEN, SPEC, czułość ważona, problem brakującej etykiety.
10. [Ściąga wzorów (skrót)](10_sciaga_wzory.md)

## Jak korzystać
- Najpierw przeczytaj plik teoretyczny danego zagadnienia.
- Następnie prześledź odpowiednie rozwiązanie z folderu [`../rozwiazania`](../rozwiazania).
- Mapę „temat → zadania" znajdziesz na końcu każdego pliku tematycznego.
