# Rozwiązane przykładowe zadania

Zadania są wzorowane na zakresie z `Wskazowki.md`. Pokazują nie tylko odpowiedź, ale też tok rozumowania, który warto umieć odtworzyć na zaliczeniu.

---

## Zadanie 1. Pytanie zamknięte - walidacja krzyżowa

**Pytanie:** Po co stosuje się k-krotną walidację krzyżową?

A. Aby nauczyć model na zbiorze testowym.  
B. Aby stabilniej oszacować jakość modelu i wykorzystać dane w kilku podziałach trening/walidacja.  
C. Aby usunąć potrzebę zbioru treningowego.  
D. Aby zawsze zwiększyć liczbę cech.

**Odpowiedź:** B.

**Wyjaśnienie:** W k-fold cross-validation dane dzieli się na `k` części. Każda część raz pełni rolę walidacyjną, a pozostałe są treningowe. Wyniki są uśredniane, co daje stabilniejszą ocenę niż pojedynczy podział.

---

## Zadanie 2. Pytanie zamknięte - overfitting

**Pytanie:** Który objaw najczęściej wskazuje na overfitting?

A. Wysoki błąd treningowy i wysoki błąd walidacyjny.  
B. Niski błąd treningowy i wysoki błąd walidacyjny.  
C. Identyczny wynik na treningu i walidacji.  
D. Brak parametrów w modelu.

**Odpowiedź:** B.

**Wyjaśnienie:** Overfitting oznacza, że model dopasował się zbyt mocno do danych treningowych, ale słabo generalizuje. Dlatego wynik treningowy jest dobry, a walidacyjny wyraźnie gorszy.

---

## Zadanie 3. Pytanie otwarte - parametry i hiperparametry

**Polecenie:** Wyjaśnij różnicę między parametrem modelu a hiperparametrem. Podaj po dwa przykłady.

**Rozwiązanie:**

Parametry modelu są uczone automatycznie podczas treningu. Przykładami są wagi i biasy w sieci neuronowej albo współczynniki regresji liniowej.

Hiperparametry ustala się przed treningiem albo dobiera procedurą strojenia. Przykładami są liczba sąsiadów `k` w KNN, `C` w SVM, `max_depth` w drzewie decyzyjnym i learning rate w sieci neuronowej.

**Dodatkowa uwaga:** Jeśli zmieniamy wartość ręcznie między treningami, najczęściej jest to hiperparametr. Jeśli wartość powstaje w wyniku optymalizacji funkcji kosztu, najczęściej jest to parametr.

---

## Zadanie 4. Pytanie otwarte - niezbalansowane klasy

**Polecenie:** Model do wykrywania oszustw ma accuracy 98%. Klasa oszustwa stanowi 1% danych. Czy accuracy wystarczy do oceny modelu? Uzasadnij i zaproponuj lepsze metryki.

**Rozwiązanie:**

Accuracy nie wystarczy, ponieważ przy silnym niezbalansowaniu klas model może przewidywać zawsze klasę większościową i nadal osiągać bardzo wysoką accuracy. Jeżeli tylko 1% przypadków to oszustwa, klasyfikator zawsze mówiący "brak oszustwa" uzyska około 99% accuracy, ale będzie bezużyteczny.

Lepsze metryki:

- recall dla klasy oszustwa - informuje, jaki procent oszustw wykrywamy,
- precision - informuje, jaki procent alarmów rzeczywiście jest oszustwem,
- F1-score - kompromis między precision i recall,
- PR-AUC - często lepsze niż ROC-AUC przy rzadkiej klasie pozytywnej,
- macierz pomyłek.

Można też użyć `class_weight`, oversamplingu, undersamplingu albo dobrać próg decyzyjny.

---

## Zadanie 5. Funkcje aktywacji

**Polecenie:** Porównaj ReLU, Sigmoid, Tanh i Softmax. Wskaż, gdzie najczęściej się ich używa.

**Rozwiązanie:**

| Funkcja | Zakres wartości | Typowe użycie | Najważniejsza cecha |
|---|---:|---|---|
| ReLU | `[0, +inf)` | warstwy ukryte | szybka, prosta, dobra dla głębszych sieci |
| Sigmoid | `(0, 1)` | prawdopodobieństwo klasy pozytywnej | dobra interpretacja probabilistyczna, ale może mieć zanik gradientu |
| Tanh | `(-1, 1)` | czasem warstwy ukryte | wartości wycentrowane wokół zera, ale też może się nasycać |
| Softmax | wartości dodatnie sumujące się do 1 | interpretacja wyników klasyfikacji wieloklasowej | zamienia logity wielu klas na rozkład prawdopodobieństwa |

W PyTorch przy `CrossEntropyLoss` model powinien zwracać logity, więc nie dodajemy `Softmax` przed funkcją kosztu. Przy klasyfikacji binarnej wygodnie używa się `BCEWithLogitsLoss`, więc podczas treningu nie trzeba dodawać `Sigmoid` w modelu.

---

## Zadanie 6. Projekt eksperymentu - klasyfikacja binarna

**Polecenie:** Zaprojektuj eksperyment dla problemu przewidywania, czy klient zrezygnuje z usługi. Dane są tabelaryczne, zawierają cechy liczbowe i kategoryczne. Klasa pozytywna stanowi 12% obserwacji.

**Rozwiązanie:**

### 1. Typ problemu

Jest to klasyfikacja binarna, bo przewidujemy jedną z dwóch klas: klient zrezygnuje albo nie zrezygnuje.

### 2. Podział danych

Użyłbym podziału stratyfikowanego, np. 70/15/15 na train/validation/test, żeby zachować proporcję klasy pozytywnej. Alternatywnie można użyć 5-krotnej walidacji krzyżowej na zbiorze treningowym.

### 3. Preprocessing

- imputacja braków danych,
- skalowanie cech liczbowych dla KNN, SVM i regresji logistycznej,
- kodowanie cech kategorycznych, np. one-hot encoding,
- wszystkie kroki w pipeline, żeby uniknąć wycieku danych.

### 4. Modele

Porównałbym:

- regresję logistyczną jako model bazowy,
- Random Forest,
- Gradient Boosting,
- SVM z jądrem RBF dla mniejszego zbioru,
- KNN jako prosty punkt odniesienia.

### 5. Metryki

Ze względu na niezbalansowanie klas nie opierałbym się tylko na accuracy. Użyłbym:

- F1-score,
- recall klasy rezygnujących,
- precision,
- PR-AUC,
- macierzy pomyłek.

### 6. Funkcja kosztu

Dla modeli probabilistycznych: binary cross-entropy/log loss. Dla PyTorch: `BCEWithLogitsLoss`, ewentualnie z wagą klasy pozytywnej.

### 7. Hiperparametry

Przykładowo:

- Logistic Regression: `C`, `penalty`, `class_weight`,
- Random Forest: `n_estimators`, `max_depth`, `max_features`, `class_weight`,
- Gradient Boosting: `learning_rate`, `n_estimators`, `max_depth`,
- SVM: `C`, `gamma`, `kernel`.

### 8. Wybór modelu

Hiperparametry dobrałbym przez random search z walidacją krzyżową. Końcowy wynik raportowałbym tylko raz na zbiorze testowym.

---

## Zadanie 7. Projekt eksperymentu - regresja

**Polecenie:** Zaprojektuj eksperyment przewidywania ceny mieszkania na podstawie danych tabelarycznych.

**Rozwiązanie:**

### Typ problemu

To regresja, ponieważ zmienna docelowa jest liczbą rzeczywistą - ceną mieszkania.

### Dane i preprocessing

Sprawdziłbym:

- braki danych,
- wartości odstające,
- rozkład ceny,
- cechy kategoryczne, np. dzielnica,
- cechy liczbowe, np. metraż, liczba pokoi, odległość od centrum.

Preprocessing:

- imputacja braków,
- one-hot encoding dla kategorii,
- skalowanie dla modeli wrażliwych na skalę, np. Ridge, Lasso, KNN, SVR.

### Modele

Porównałbym:

- regresję liniową jako baseline,
- Ridge/Lasso/Elastic Net,
- KNN Regressor,
- Random Forest Regressor,
- Gradient Boosting Regressor,
- SVR dla mniejszego zbioru.

### Funkcje kosztu i metryki

Do uczenia można użyć MSE, a do raportowania:

- MAE - średni błąd w jednostce ceny,
- RMSE - mocniej karze duże pomyłki,
- R2 - wyjaśniona część wariancji.

Jeśli występują duże wartości odstające, MAE albo Huber loss mogą być bardziej odporne.

### Strojenie

Przykładowe hiperparametry:

- Ridge/Lasso: `alpha`,
- Random Forest: `n_estimators`, `max_depth`, `min_samples_leaf`,
- Gradient Boosting: `learning_rate`, `n_estimators`, `max_depth`,
- SVR: `C`, `epsilon`, `gamma`.

Wynik końcowy oceniłbym na zbiorze testowym niewykorzystywanym do strojenia.

---

## Zadanie 8. Dobór funkcji kosztu

**Polecenie:** Dobierz funkcję kosztu do trzech problemów:

1. przewidywanie temperatury jutro,
2. wykrywanie spamu,
3. rozpoznawanie jednej z dziesięciu cyfr.

**Rozwiązanie:**

1. Przewidywanie temperatury to regresja. Można użyć MSE, MAE albo Huber loss. MSE mocniej karze duże błędy.
2. Wykrywanie spamu to klasyfikacja binarna. Standardem jest binary cross-entropy. W PyTorch dobrym wyborem jest `BCEWithLogitsLoss`.
3. Rozpoznawanie jednej z dziesięciu cyfr to klasyfikacja wieloklasowa. Standardem jest cross-entropy. W PyTorch używa się `CrossEntropyLoss`.

---

## Zadanie 9. Implementacja PyTorch - klasyfikacja wieloklasowa

**Polecenie:** Napisz model z warstwami liniowymi dla danych tabelarycznych z 16 cechami wejściowymi i 3 klasami. Dobierz funkcję kosztu i optymalizator.

**Rozwiązanie:**

```python
import torch
from torch import nn

class Net(nn.Module):
    def __init__(self):
        super().__init__()
        self.layers = nn.Sequential(
            nn.Linear(16, 64),
            nn.ReLU(),
            nn.BatchNorm1d(64),
            nn.Dropout(p=0.2),
            nn.Linear(64, 32),
            nn.ReLU(),
            nn.Linear(32, 3),
        )

    def forward(self, x):
        return self.layers(x)

model = Net()
criterion = nn.CrossEntropyLoss()
optimizer = torch.optim.Adam(model.parameters(), lr=1e-3)
```

**Wyjaśnienie:**

Model zwraca 3 logity, po jednym dla każdej klasy. `CrossEntropyLoss` sama łączy log-softmax i negative log likelihood, dlatego nie dodajemy `Softmax` w ostatniej warstwie podczas treningu.

---

## Zadanie 10. Implementacja PyTorch - regresja

**Polecenie:** Napisz model dla regresji z 8 cechami wejściowymi. Model ma mieć dwie warstwy ukryte. Dobierz funkcję kosztu i optymalizator.

**Rozwiązanie:**

```python
import torch
from torch import nn

class RegressionModel(nn.Module):
    def __init__(self):
        super().__init__()
        self.net = nn.Sequential(
            nn.Linear(8, 32),
            nn.ReLU(),
            nn.Linear(32, 16),
            nn.ReLU(),
            nn.Linear(16, 1),
        )

    def forward(self, x):
        return self.net(x)

model = RegressionModel()
criterion = nn.MSELoss()
optimizer = torch.optim.Adam(model.parameters(), lr=1e-3)
```

**Wyjaśnienie:**

Regresja wymaga pojedynczego wyjścia liczbowego. Nie stosujemy sigmoidy ani softmaxu na końcu, bo wynik nie jest klasą ani prawdopodobieństwem.

---

## Zadanie 11. Bias-variance

**Polecenie:** Model A ma podobnie słaby wynik na treningu i walidacji. Model B ma bardzo dobry wynik na treningu, ale słaby na walidacji. Zinterpretuj oba przypadki.

**Rozwiązanie:**

Model A prawdopodobnie ma underfitting, czyli wysoki bias. Jest zbyt prosty, zbyt mocno regularyzowany albo uczony zbyt krótko.

Model B prawdopodobnie ma overfitting, czyli wysoką wariancję. Dopasował się do danych treningowych, ale nie generalizuje.

Możliwe działania:

- dla modelu A: zwiększyć złożoność, poprawić cechy, trenować dłużej, zmniejszyć regularyzację,
- dla modelu B: dodać regularyzację, użyć early stopping, dropout, augmentacji, prostszego modelu albo zebrać więcej danych.

---

## Zadanie 12. Bagging, boosting, stacking

**Polecenie:** Wyjaśnij różnice między baggingiem, boostingiem i stackingiem.

**Rozwiązanie:**

Bagging uczy wiele modeli niezależnie na losowych próbkach danych i uśrednia predykcje. Przykładem jest Random Forest. Główny efekt to zmniejszenie wariancji.

Boosting uczy modele sekwencyjnie. Kolejne modele poprawiają błędy poprzednich. Przykładami są AdaBoost i Gradient Boosting. Może osiągać bardzo dobre wyniki, ale wymaga kontroli overfittingu.

Stacking uczy kilka różnych modeli bazowych, a następnie metamodel, który łączy ich predykcje. Trzeba uważać, żeby metamodel był uczony na predykcjach walidacyjnych, nie na predykcjach z tych samych danych treningowych, bo grozi to wyciekiem danych.

