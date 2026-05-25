# Zestaw zadań 2 - bez rozwiązań

Drugi zestaw służy do niezależnego przećwiczenia tych samych zagadnień w innych kontekstach. Nie zawiera odpowiedzi.

## Część A. Zadania zamknięte jednokrotnego wyboru

### 1. Podział danych

Po co wydziela się zbiór testowy?

A. Do strojenia hiperparametrów w każdej epoce.  
B. Do końcowej oceny modelu po zakończeniu wyboru modelu i hiperparametrów.  
C. Do uczenia parametrów modelu.  
D. Do zastąpienia funkcji kosztu.

### 2. Spadek gradientu

Co robi metoda spadku gradientu?

A. Aktualizuje parametry w kierunku przeciwnym do gradientu funkcji kosztu.  
B. Losowo usuwa cechy ze zbioru testowego.  
C. Zamienia klasyfikację w regresję.  
D. Oblicza wyłącznie metrykę accuracy.

### 3. Dropout

Jaki jest główny cel dropout?

A. Przyspieszenie odczytu danych z dysku.  
B. Losowe zerowanie części aktywacji podczas treningu w celu regularyzacji.  
C. Zamiana logitów na prawdopodobieństwa.  
D. Normalizacja etykiet klas.

### 4. Batch normalization

Które zdanie najlepiej opisuje batch normalization?

A. Normalizuje aktywacje w mini-batchu i może stabilizować uczenie.  
B. Zawsze zastępuje funkcję kosztu.  
C. Działa wyłącznie w modelach KNN.  
D. Służy tylko do podziału danych na train/test.

### 5. Random search

Na czym polega random search?

A. Sprawdza wszystkie możliwe kombinacje hiperparametrów z siatki.  
B. Losuje kombinacje hiperparametrów z zadanych zakresów lub rozkładów.  
C. Uczy model bez danych treningowych.  
D. Zawsze wybiera najmniejszy model.

### 6. Klasyfikacja binarna w PyTorch

Która funkcja kosztu jest zwykle odpowiednia, gdy model zwraca jeden logit dla klasyfikacji binarnej?

A. `nn.CrossEntropyLoss()` z jedną klasą.  
B. `nn.BCEWithLogitsLoss()`.  
C. `nn.MSELoss()` zawsze i bez wyjątków.  
D. `nn.Softmax()`.

---

## Część B. Krótkie zadania otwarte

### 7. Funkcje kosztu

Dobierz funkcję kosztu do problemów:

1. przewidywanie zużycia energii w kWh,
2. klasyfikacja wiadomości jako spam/nie-spam,
3. rozpoznanie gatunku rośliny spośród pięciu klas.

Uzasadnij każdy wybór.

### 8. Algorytmy strojenia hiperparametrów

Porównaj grid search, random search i optymalizację bayesowską. Wskaż zalety i ograniczenia każdej metody.

---

## Część C. Funkcje aktywacji

### 9. Dobór aktywacji do wyjścia modelu

Wyjaśnij, jak dobrać ostatnią warstwę i funkcję aktywacji lub funkcję kosztu dla:

1. regresji,
2. klasyfikacji binarnej,
3. klasyfikacji wieloklasowej.

Uwzględnij przypadek użycia `BCEWithLogitsLoss` i `CrossEntropyLoss` w PyTorch.

---

## Część D. Projekt eksperymentu z modelami płytkimi

### 10. Regresja

Masz dane o samochodach i chcesz przewidzieć ich cenę. Dane zawierają cechy liczbowe, cechy kategoryczne oraz wartości odstające.

Zaprojektuj eksperyment. Uwzględnij:

1. typ problemu,
2. preprocessing,
3. podział danych albo walidację krzyżową,
4. co najmniej cztery modele płytkie,
5. funkcje kosztu i metryki,
6. hiperparametry do strojenia,
7. sposób oceny wpływu wartości odstających,
8. końcową procedurę wyboru modelu.

---

## Część E. Implementacja modelu głębokiego w PyTorch

### 11. Klasyfikacja wieloklasowa

Napisz kod modelu PyTorch dla danych tabelarycznych:

- liczba cech wejściowych: 25,
- liczba klas: 5,
- co najmniej dwie warstwy liniowe,
- użyj ReLU,
- dodaj batch normalization,
- dobierz ostatnią warstwę,
- dobierz funkcję kosztu i optymalizator.

Nie musisz pisać pełnej pętli treningowej.

---

## Część F. Dodatkowe pytania problemowe

### 12. Augmentacja danych

Wyjaśnij, czym jest augmentacja danych. Podaj przykłady augmentacji dla obrazów i napisz, dlaczego augmentację wykonuje się zwykle tylko na zbiorze treningowym.

### 13. Backpropagation

Opisz krótko etapy uczenia sieci neuronowej z użyciem backpropagation i optymalizatora.

### 14. Stacking

Wyjaśnij, czym jest stacking. Dlaczego podczas uczenia metamodelu trzeba uważać na wyciek danych?

### 15. Dobór modeli płytkich

Dla każdego problemu wskaż po dwa sensowne modele płytkie i po dwa hiperparametry do strojenia:

1. klasyfikacja binarna klientów odchodzących z usługi,
2. klasyfikacja wieloklasowa typów dokumentów,
3. regresja ceny nieruchomości.

