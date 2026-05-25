# Zestaw zadań 1 - bez rozwiązań

Zestaw jest przeznaczony do samodzielnego powtórzenia materiału. Nie zawiera odpowiedzi.

## Część A. Zadania zamknięte jednokrotnego wyboru

### 1. K-krotna walidacja krzyżowa

Które zdanie najlepiej opisuje k-krotną walidację krzyżową?

A. Model jest uczony tylko raz na zbiorze testowym.
B. Dane są dzielone na `k` części, a każda część raz pełni rolę walidacyjną.
C. K-krotna walidacja zawsze usuwa overfitting.
D. K-krotna walidacja służy tylko do augmentacji obrazów.

### 2. Regularyzacja L1

Jaki efekt jest szczególnie charakterystyczny dla regularyzacji L1?

A. Może wyzerować część wag modelu.
B. Zawsze zwiększa liczbę cech.
C. Działa wyłącznie w klasyfikacji wieloklasowej.
D. Jest tym samym co batch normalization.

### 3. KNN

Dlaczego przy KNN zwykle warto skalować cechy?

A. Bo KNN używa odległości między próbkami.
B. Bo KNN nie obsługuje danych liczbowych.
C. Bo skalowanie zastępuje walidację.
D. Bo KNN wymaga funkcji softmax.

### 4. SVM

Co zwykle oznacza większa wartość hiperparametru `C` w SVM?

A. Silniejszą regularyzację i szerszy margines kosztem większej liczby błędów.
B. Mniejszą karę za błędy.
C. Większą karę za błędy i potencjalnie bardziej dopasowaną granicę.
D. Liczbę klas w problemie.

### 5. Niezbalansowane klasy

Która metryka bywa myląca przy silnie niezbalansowanych klasach?

A. Recall.
B. Precision.
C. Accuracy.
D. F1-score.

### 6. Funkcja kosztu

Która funkcja kosztu jest typowym wyborem dla klasyfikacji wieloklasowej z jedną poprawną klasą?

A. MSELoss.
B. Cross-entropy.
C. MAE.
D. Huber loss.

---

## Część B. Krótkie zadania otwarte

### 7. Parametry i hiperparametry

Wyjaśnij różnicę między parametrem modelu a hiperparametrem. Podaj po dwa przykłady każdego z nich.

### 8. Overfitting i underfitting

Opisz różnicę między overfittingiem i underfittingiem. Podaj po dwa sposoby przeciwdziałania każdemu z nich.

---

## Część C. Funkcje aktywacji

### 9. ReLU, Sigmoid, Tanh, Softmax

Porównaj funkcje aktywacji ReLU, Sigmoid, Tanh i Softmax. W odpowiedzi uwzględnij:

- zakres wartości,
- typowe zastosowanie,
- jedną zaletę albo ograniczenie każdej funkcji.

---

## Część D. Projekt eksperymentu z modelami płytkimi

### 10. Klasyfikacja binarna

Masz dane tabelaryczne banku i chcesz przewidzieć, czy klient spłaci kredyt. Klasa niespłacających kredytu stanowi 8% obserwacji.

Zaprojektuj eksperyment. Uwzględnij:

1. typ problemu,
2. sposób podziału danych,
3. preprocessing,
4. co najmniej trzy modele płytkie,
5. funkcję kosztu lub kryterium uczenia,
6. metryki oceny,
7. przykładowe hiperparametry do strojenia,
8. sposób radzenia sobie z niezbalansowaniem klas.

---

## Część E. Implementacja modelu głębokiego w PyTorch

### 11. Klasyfikacja binarna

Napisz kod modelu PyTorch dla klasyfikacji binarnej danych tabelarycznych:

- liczba cech wejściowych: 12,
- dwie warstwy ukryte,
- użyj ReLU,
- dodaj dropout,
- dobierz odpowiednią ostatnią warstwę,
- dobierz funkcję kosztu i optymalizator.

Nie musisz pisać pełnej pętli treningowej.

---

## Część F. Dodatkowe pytania problemowe

### 12. Early stopping

Wyjaśnij, czym jest early stopping. Jakie informacje z procesu uczenia są potrzebne, żeby go zastosować?

### 13. Bagging i boosting

Porównaj bagging i boosting. Podaj po jednym przykładzie algorytmu dla każdej techniki.

### 14. Bias-variance trade-off

Wyjaśnij kompromis bias-variance. Jak zmieniają się bias i variance, gdy zwiększamy złożoność modelu?
