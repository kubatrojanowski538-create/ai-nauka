# Materiały do nauki - zaliczenie laboratorium ze Sztucznej Inteligencji

## Jak korzystać z materiałów

Zakres wynika z pliku `Wskazowki.md`. Na zaliczeniu pojawiają się pytania zamknięte, krótkie pytania otwarte, zadanie o funkcjach aktywacji, projekt eksperymentu z modelami płytkimi oraz implementacja prostego modelu głębokiego w PyTorch.

Najważniejsze umiejętności:

- rozpoznanie, czy problem jest regresją, klasyfikacją binarną czy wieloklasową,
- dobranie podziału danych, walidacji, metryk i funkcji kosztu,
- rozumienie przeuczenia, niedouczenia i kompromisu bias-variance,
- wskazanie sensownych modeli płytkich oraz hiperparametrów,
- zaprojektowanie eksperymentu uczenia maszynowego,
- zbudowanie prostej sieci neuronowej z warstw liniowych.

---

## 1. Podział danych na podzbiory

Typowy podział danych:

- **zbiór treningowy** - służy do uczenia parametrów modelu,
- **zbiór walidacyjny** - służy do wyboru hiperparametrów i decyzji projektowych,
- **zbiór testowy** - służy do końcowej, możliwie bezstronnej oceny modelu.

Przykładowy podział: 70% trening, 15% walidacja, 15% test. Dla małych zbiorów częściej stosuje się walidację krzyżową.

W klasyfikacji warto użyć podziału **stratyfikowanego**, czyli zachowującego proporcje klas w każdym podzbiorze.

---

## 2. K-krotna walidacja krzyżowa

**K-fold cross-validation** polega na podziale danych na `k` części. Model uczony jest `k` razy: za każdym razem jedna część jest walidacyjna, a pozostałe są treningowe. Wyniki uśrednia się.

Zalety:

- lepsze wykorzystanie małego zbioru danych,
- stabilniejsza ocena jakości modelu niż pojedynczy podział,
- możliwość porównania hiperparametrów.

Wady:

- większy koszt obliczeniowy,
- trzeba uważać na wyciek danych, np. skalowanie musi być dopasowane tylko na części treningowej w danym foldzie.

Typowe wartości: `k = 5` lub `k = 10`.

---

## 3. Parametry modelu a hiperparametry

**Parametry modelu** są wyznaczane podczas uczenia, np. wagi w regresji liniowej lub sieci neuronowej.

**Hiperparametry** ustawia osoba projektująca eksperyment przed uczeniem albo są dobierane przez procedurę strojenia, np. `k` w KNN, `C` w SVM, `max_depth` w drzewie decyzyjnym, learning rate w sieci neuronowej.

---

## 4. Algorytmy poszukiwania hiperparametrów

### Grid search

Sprawdza wszystkie kombinacje z ustalonej siatki wartości.

- plus: prosty i systematyczny,
- minus: kosztowny przy wielu hiperparametrach.

### Random search

Losuje kombinacje hiperparametrów z zadanych rozkładów.

- plus: często efektywniejszy niż grid search,
- minus: wynik zależy od losowania i liczby prób.

### Bayesian optimization

Buduje model zależności między hiperparametrami a wynikiem i wybiera kolejne próby w bardziej świadomy sposób.

- plus: dobra metoda przy drogim uczeniu modeli,
- minus: bardziej złożona.

---

## 5. Metoda spadku gradientu

Spadek gradientu minimalizuje funkcję kosztu przez aktualizację parametrów w kierunku przeciwnym do gradientu.

Ogólna aktualizacja:

```text
w := w - learning_rate * gradient
```

### Batch Gradient Descent (GD)

Gradient liczony jest na całym zbiorze treningowym.

- stabilniejszy kierunek aktualizacji,
- wolny dla dużych zbiorów.

### Stochastic Gradient Descent (SGD)

Gradient liczony jest dla jednej próbki albo małego batcha.

- szybszy i tańszy na dużych danych,
- bardziej szumiący przebieg uczenia,
- może pomagać uciec z płytkich minimów lokalnych.

Najważniejszy hiperparametr: **learning rate**. Zbyt duży może powodować rozbieganie uczenia, zbyt mały bardzo wolną naukę.

---

## 6. Funkcje kosztu i ich dobór

### Regresja

- **MSE** - średni błąd kwadratowy; mocno karze duże błędy.
- **MAE** - średni błąd bezwzględny; odporniejszy na wartości odstające.
- **Huber loss** - kompromis między MSE i MAE.

### Klasyfikacja binarna

- **Binary cross-entropy / log loss** - standard dla prawdopodobieństwa klasy pozytywnej.
- W PyTorch często używa się `BCEWithLogitsLoss`, gdy model zwraca logity bez sigmoidy.

### Klasyfikacja wieloklasowa

- **Cross-entropy loss** - standard dla jednej poprawnej klasy spośród wielu.
- W PyTorch `CrossEntropyLoss` oczekuje logitów i indeksów klas, więc zwykle nie dodaje się `Softmax` na końcu modelu treningowego.

---

## 7. Overfitting i underfitting

### Overfitting - przeuczenie

Model za dobrze dopasowuje się do danych treningowych, ale słabo generalizuje.

Objawy:

- niski błąd treningowy,
- wysoki błąd walidacyjny/testowy,
- duża różnica między wynikiem treningowym i walidacyjnym.

Sposoby ograniczania:

- regularyzacja L1/L2,
- dropout,
- early stopping,
- augmentacja danych,
- prostszy model,
- więcej danych,
- walidacja krzyżowa.

### Underfitting - niedouczenie

Model jest za prosty albo źle uczony i nie potrafi uchwycić zależności.

Objawy:

- wysoki błąd treningowy,
- wysoki błąd walidacyjny,
- słabe wyniki nawet na danych treningowych.

Sposoby ograniczania:

- bardziej złożony model,
- dłuższe uczenie,
- lepsze cechy,
- zmniejszenie zbyt silnej regularyzacji,
- zmiana funkcji aktywacji lub architektury.

---

## 8. Bias-variance trade-off

**Bias** to błąd wynikający z uproszczonych założeń modelu. Wysoki bias sprzyja underfittingowi.

**Variance** to wrażliwość modelu na konkretne dane treningowe. Wysoka wariancja sprzyja overfittingowi.

Kompromis:

- prosty model: zwykle większy bias, mniejsza wariancja,
- złożony model: zwykle mniejszy bias, większa wariancja.

Celem jest model, który dobrze generalizuje, a nie tylko dobrze zapamiętuje trening.

---

## 9. Regularyzacja L1 i L2

Regularyzacja dodaje karę do funkcji kosztu, żeby ograniczyć złożoność modelu.

### L1

Kara za sumę wartości bezwzględnych wag.

Efekty:

- może zerować część wag,
- działa jak selekcja cech,
- przydatna przy wielu cechach, z których część jest nieistotna.

### L2

Kara za sumę kwadratów wag.

Efekty:

- zmniejsza wartości wag,
- stabilizuje model,
- zwykle nie zeruje wag całkowicie.

W scikit-learn siła regularyzacji często występuje jako `alpha` albo odwrotnie jako `C`, gdzie mniejsze `C` oznacza silniejszą regularyzację.

---

## 10. KNN

**K-nearest neighbors** klasyfikuje lub przewiduje wartość na podstawie najbliższych przykładów treningowych.

Najważniejsze hiperparametry:

- `n_neighbors` / `k` - liczba sąsiadów,
- `weights` - głosowanie równe lub ważone odległością,
- `metric` - metryka odległości, np. euklidesowa, Manhattan.

Ważne:

- wymaga skalowania cech,
- mało uczy się w fazie treningu, ale może być kosztowny w predykcji,
- małe `k` zwiększa wariancję, duże `k` zwiększa bias.

---

## 11. SVM

**Support Vector Machine** szuka granicy decyzyjnej maksymalizującej margines między klasami. W regresji wariantem jest SVR.

Najważniejsze hiperparametry:

- `C` - kara za błędy; duże `C` oznacza mniejszą regularyzację i większe ryzyko overfittingu,
- `kernel` - typ granicy, np. `linear`, `rbf`, `poly`,
- `gamma` - wpływ pojedynczych punktów w jądrze RBF; duże `gamma` daje bardziej lokalne, złożone granice.

Ważne:

- wymaga skalowania cech,
- dobrze działa w przestrzeniach o wielu wymiarach,
- dla dużych zbiorów może być kosztowny.

---

## 12. Niezbalansowanie klas

Niezbalansowanie występuje, gdy jedna klasa jest dużo częstsza od innych, np. 95% klasy 0 i 5% klasy 1.

Ryzyka:

- accuracy może być mylące,
- model może ignorować klasę mniejszościową.

Lepsze metryki:

- precision,
- recall,
- F1-score,
- ROC-AUC,
- PR-AUC,
- macierz pomyłek.

Sposoby radzenia sobie:

- `class_weight`,
- oversampling klasy mniejszościowej,
- undersampling klasy większościowej,
- SMOTE,
- dobranie progu decyzyjnego,
- stratyfikowany podział danych.

---

## 13. Bagging, boosting i stacking

### Bagging

Uczy wiele modeli na losowych próbkach danych i uśrednia ich predykcje.

Przykład: Random Forest.

Efekt: zmniejsza wariancję i ogranicza overfitting pojedynczego modelu.

### Boosting

Uczy modele sekwencyjnie, a kolejne modele skupiają się na błędach poprzednich.

Przykłady: AdaBoost, Gradient Boosting, XGBoost, LightGBM, CatBoost.

Efekt: może dawać bardzo wysoką jakość, ale wymaga strojenia i może się przeuczać.

### Stacking

Łączy predykcje różnych modeli bazowych przy pomocy metamodelu.

Ważne: metamodel powinien być uczony na predykcjach walidacyjnych, żeby uniknąć wycieku danych.

---

## 14. Early stopping

Early stopping zatrzymuje uczenie, gdy wynik walidacyjny przestaje się poprawiać.

Przydatne w:

- sieciach neuronowych,
- gradient boostingu,
- długim uczeniu iteracyjnym.

Najważniejsze parametry:

- monitorowana metryka, np. validation loss,
- `patience` - ile epok bez poprawy tolerujemy,
- minimalna wymagana poprawa.

---

## 15. Augmentacja danych

Augmentacja sztucznie zwiększa różnorodność danych treningowych przez transformacje zachowujące etykietę.

Przykłady dla obrazów:

- obroty,
- przycięcia,
- odbicia,
- zmiana jasności,
- szum.

Cel:

- ograniczenie overfittingu,
- poprawa generalizacji,
- zwiększenie odporności modelu.

---

## 16. Backpropagation

Backpropagation oblicza gradient funkcji kosztu względem wag sieci neuronowej, przechodząc od wyjścia do wejścia zgodnie z regułą łańcuchową.

Kroki:

1. Forward pass - model oblicza predykcję.
2. Obliczenie funkcji kosztu.
3. Backward pass - obliczenie gradientów.
4. Aktualizacja wag przez optymalizator.

W PyTorch odpowiadają temu m.in.:

```python
loss = criterion(outputs, targets)
optimizer.zero_grad()
loss.backward()
optimizer.step()
```

---

## 17. Dropout

Dropout podczas treningu losowo zeruje część aktywacji neuronów.

Efekty:

- ogranicza współzależność neuronów,
- działa jak regularyzacja,
- zmniejsza overfitting.

Hiperparametr `p` oznacza prawdopodobieństwo wyzerowania aktywacji. Typowe wartości to `0.1-0.5`.

Podczas ewaluacji dropout jest wyłączany, dlatego trzeba używać:

```python
model.train()  # trening
model.eval()   # walidacja/test
```

---

## 18. Batch normalization

Batch normalization normalizuje aktywacje w mini-batchu i uczy dodatkowe parametry skali oraz przesunięcia.

Efekty:

- stabilniejsze uczenie,
- możliwość użycia większego learning rate,
- czasem lekkie działanie regularyzujące.

W sieciach z warstwami liniowymi używa się zwykle `nn.BatchNorm1d`.

---

## 19. Funkcje aktywacji

### ReLU

```text
f(x) = max(0, x)
```

Zastosowanie: najczęstsza funkcja w warstwach ukrytych.

Zalety:

- prosta i szybka,
- ogranicza problem zanikającego gradientu dla dodatnich wartości.

Wada: neurony mogą "umrzeć", jeśli stale zwracają 0.

### Sigmoid

```text
f(x) = 1 / (1 + exp(-x))
```

Zastosowanie: interpretacja wyniku jako prawdopodobieństwa klasy pozytywnej w klasyfikacji binarnej.

Wady:

- nasyca się dla dużych wartości,
- może powodować zanik gradientu.

### Tanh

Zwraca wartości z zakresu `(-1, 1)`.

Zastosowanie: czasem w warstwach ukrytych, szczególnie gdy przydatne są wartości ujemne i dodatnie.

Wada: również może się nasycać.

### Softmax

Zamienia logity wielu klas na rozkład prawdopodobieństwa sumujący się do 1.

Zastosowanie: klasyfikacja wieloklasowa podczas interpretacji wyniku.

Uwaga: przy `nn.CrossEntropyLoss` w PyTorch nie dodajemy softmaxu w modelu przed funkcją kosztu.

---

## 20. Prosty model głęboki w PyTorch

### Regresja tabelaryczna

Wyjście: jedna liczba.

Funkcja kosztu: `nn.MSELoss()` albo `nn.L1Loss()`.

```python
import torch
from torch import nn

class RegressionNet(nn.Module):
    def __init__(self, input_dim: int):
        super().__init__()
        self.net = nn.Sequential(
            nn.Linear(input_dim, 64),
            nn.ReLU(),
            nn.Linear(64, 32),
            nn.ReLU(),
            nn.Linear(32, 1),
        )

    def forward(self, x):
        return self.net(x)

model = RegressionNet(input_dim=10)
criterion = nn.MSELoss()
optimizer = torch.optim.Adam(model.parameters(), lr=1e-3)
```

### Klasyfikacja binarna

Wyjście: jeden logit.

Funkcja kosztu: `nn.BCEWithLogitsLoss()`.

```python
class BinaryClassifier(nn.Module):
    def __init__(self, input_dim: int):
        super().__init__()
        self.net = nn.Sequential(
            nn.Linear(input_dim, 64),
            nn.ReLU(),
            nn.Dropout(p=0.2),
            nn.Linear(64, 1),
        )

    def forward(self, x):
        return self.net(x).squeeze(1)

model = BinaryClassifier(input_dim=20)
criterion = nn.BCEWithLogitsLoss()
optimizer = torch.optim.Adam(model.parameters(), lr=1e-3)
```

Predykcja klasy:

```python
proba = torch.sigmoid(logits)
pred = (proba >= 0.5).long()
```

### Klasyfikacja wieloklasowa

Wyjście: liczba logitów równa liczbie klas.

Funkcja kosztu: `nn.CrossEntropyLoss()`.

```python
class MulticlassClassifier(nn.Module):
    def __init__(self, input_dim: int, num_classes: int):
        super().__init__()
        self.net = nn.Sequential(
            nn.Linear(input_dim, 128),
            nn.ReLU(),
            nn.BatchNorm1d(128),
            nn.Linear(128, 64),
            nn.ReLU(),
            nn.Linear(64, num_classes),
        )

    def forward(self, x):
        return self.net(x)

model = MulticlassClassifier(input_dim=30, num_classes=4)
criterion = nn.CrossEntropyLoss()
optimizer = torch.optim.Adam(model.parameters(), lr=1e-3)
```

---

## 21. Modele płytkie według typu problemu

Poniższe tabele zawierają modele, które warto umieć dobrać do eksperymentu. Zakresy hiperparametrów są orientacyjne i należy je dostosować do danych.

### Regresja

| Model | Kiedy użyć | Hiperparametry | Na co wpływają |
|---|---|---|---|
| Regresja liniowa | Prosta zależność liniowa, model bazowy | `fit_intercept` (`True/False`), `positive` (`True/False`) | `fit_intercept` dodaje wyraz wolny; `positive` wymusza nieujemne współczynniki |
| Ridge | Regresja liniowa z regularyzacją L2 | `alpha` (`1e-4-100`), `solver`, `fit_intercept` | większe `alpha` silniej zmniejsza wagi i ogranicza overfitting; `solver` wpływa na sposób optymalizacji |
| Lasso | Regresja liniowa z regularyzacją L1 | `alpha` (`1e-4-10`), `max_iter`, `selection` | większe `alpha` może zerować cechy; `max_iter` wpływa na zbieżność |
| Elastic Net | Połączenie L1 i L2 | `alpha`, `l1_ratio` (`0-1`), `max_iter` | `l1_ratio` kontroluje udział L1 względem L2; `alpha` kontroluje siłę kary |
| KNN Regressor | Lokalne zależności, małe/średnie zbiory | `n_neighbors` (`3-50`), `weights`, `metric` | większe `n_neighbors` wygładza predykcje; `weights='distance'` wzmacnia bliskich sąsiadów |
| Decision Tree Regressor | Nieliniowe zależności, interpretowalność | `max_depth`, `min_samples_leaf`, `min_samples_split` | większa głębokość zwiększa złożoność; większe minima próbek ograniczają overfitting |
| Random Forest Regressor | Mocny model bazowy dla danych tabelarycznych | `n_estimators` (`100-1000`), `max_depth`, `max_features` | więcej drzew stabilizuje wynik; `max_depth` kontroluje złożoność; `max_features` zwiększa różnorodność drzew |
| Gradient Boosting Regressor | Wysoka jakość przy danych tabelarycznych | `learning_rate` (`0.01-0.2`), `n_estimators`, `max_depth` | mniejszy learning rate wymaga więcej drzew; głębsze drzewa zwiększają złożoność |
| SVR | Małe/średnie zbiory, zależności nieliniowe | `C`, `epsilon`, `kernel`, `gamma` | `C` kontroluje karę za błędy; `epsilon` szerokość marginesu błędu; `gamma` złożoność jądra RBF |

### Klasyfikacja binarna

| Model | Kiedy użyć | Hiperparametry | Na co wpływają |
|---|---|---|---|
| Logistic Regression | Mocny, interpretowalny model bazowy | `C` (`0.001-100`), `penalty` (`l1/l2/elasticnet`), `class_weight` | większe `C` słabiej reguluje; `penalty` zmienia typ kary; `class_weight` pomaga przy niezbalansowaniu |
| KNN Classifier | Proste granice lokalne, małe zbiory | `n_neighbors`, `weights`, `metric` | małe `k` zwiększa wariancję; metryka zależy od skali i typu cech |
| SVC | Granice liniowe lub nieliniowe | `C`, `kernel`, `gamma`, `class_weight` | `C` i `gamma` kontrolują złożoność; `kernel` określa kształt granicy |
| Linear SVM | Dużo cech, granica prawie liniowa | `C`, `loss`, `class_weight` | `C` reguluje margines; `class_weight` zmienia koszt błędów klas |
| Decision Tree Classifier | Interpretowalne reguły | `max_depth`, `min_samples_leaf`, `criterion` | głębokość i minimalne liście kontrolują overfitting; `criterion` zmienia miarę podziału |
| Random Forest Classifier | Stabilna klasyfikacja tabelaryczna | `n_estimators`, `max_depth`, `max_features`, `class_weight` | liczba drzew zmniejsza wariancję; głębokość kontroluje złożoność; wagi klas pomagają przy imbalance |
| AdaBoost Classifier | Prosty boosting słabych klasyfikatorów | `n_estimators`, `learning_rate`, `estimator` | więcej estymatorów i większy learning rate zwiększają dopasowanie |
| Gradient Boosting Classifier | Wysoka jakość na danych tabelarycznych | `learning_rate`, `n_estimators`, `max_depth`, `subsample` | `subsample < 1` dodaje losowość; pozostałe kontrolują tempo i złożoność uczenia |
| Naive Bayes | Tekst, proste szybkie klasyfikatory | `alpha`, `var_smoothing` zależnie od wariantu | wygładzanie zapobiega zerowym prawdopodobieństwom i stabilizuje predykcje |

### Klasyfikacja wieloklasowa

| Model | Kiedy użyć | Hiperparametry | Na co wpływają |
|---|---|---|---|
| Logistic Regression multinomial | Wieloklasowy model liniowy | `C`, `penalty`, `solver`, `multi_class` | `C` kontroluje regularyzację; `solver` musi obsługiwać wybraną karę i tryb wieloklasowy |
| KNN Classifier | Decyzja na podstawie sąsiadów wielu klas | `n_neighbors`, `weights`, `metric` | większe `k` wygładza granice; wagi odległości pomagają, gdy bliscy sąsiedzi są bardziej wiarygodni |
| SVC one-vs-one | Mniejsze/średnie zbiory, złożone granice | `C`, `kernel`, `gamma`, `decision_function_shape` | `decision_function_shape` zmienia sposób raportowania decyzji; `C/gamma` wpływają na złożoność |
| One-vs-Rest Classifier | Gdy model bazowy jest binarny | `estimator`, hiperparametry estymatora | uczy osobny klasyfikator dla każdej klasy kontra reszta |
| Decision Tree Classifier | Reguły decyzyjne dla wielu klas | `max_depth`, `min_samples_leaf`, `criterion` | kontrolują złożoność drzewa i jakość podziałów |
| Random Forest Classifier | Uniwersalny model tabelaryczny | `n_estimators`, `max_depth`, `max_features`, `class_weight` | stabilność, złożoność i obsługa niezbalansowania klas |
| Gradient Boosting / HistGradientBoosting | Mocne modele wieloklasowe dla tabel | `learning_rate`, `max_iter`/`n_estimators`, `max_leaf_nodes`, `l2_regularization` | tempo uczenia, liczba iteracji i złożoność drzew; L2 ogranicza przeuczenie |
| Gaussian Naive Bayes | Szybki model bazowy dla cech liczbowych | `var_smoothing` | stabilizuje wariancje cech i może poprawić generalizację |

---

## 22. Dobór modelu, metryki i funkcji kosztu

| Typ problemu | Wyjście modelu | Funkcja kosztu | Typowe metryki |
|---|---|---|---|
| Regresja | liczba rzeczywista | MSE, MAE, Huber | MAE, RMSE, R2 |
| Klasyfikacja binarna | prawdopodobieństwo lub logit klasy pozytywnej | binary cross-entropy | accuracy, precision, recall, F1, ROC-AUC, PR-AUC |
| Klasyfikacja wieloklasowa | wektor logitów/probabilistyczny rozkład klas | cross-entropy | accuracy, macro F1, balanced accuracy, confusion matrix |

Przy niezbalansowanych klasach nie opieraj się wyłącznie na accuracy.

---

## 23. Schemat projektowania eksperymentu z modelami płytkimi

1. Opisz problem: regresja, klasyfikacja binarna albo wieloklasowa.
2. Opisz dane: liczba próbek, cechy, typy zmiennych, braki danych, rozkład klas.
3. Ustal podział danych: train/validation/test albo k-fold.
4. Przygotuj preprocessing:
   - imputacja braków,
   - kodowanie kategorii,
   - skalowanie dla KNN/SVM/regresji logistycznej,
   - pipeline bez wycieku danych.
5. Wybierz modele bazowe.
6. Dobierz funkcję kosztu i metryki.
7. Ustal przestrzeń hiperparametrów.
8. Przeprowadź strojenie, np. random search z cross-validation.
9. Wybierz model na podstawie walidacji.
10. Oceń raz na zbiorze testowym.
11. Zinterpretuj błędy i ograniczenia.
