# 8. GEP — Gene Expression Programming

## 8.1. Idea
GEP koduje wyrażenia (drzewa) w postaci **liniowych chromosomów** o stałej długości. Łączy zalety GA (proste, liniowe genotypy) i programowania genetycznego (drzewiaste fenotypy).

## 8.2. Budowa genu (K-wyrażenie, notacja Karva)
- Gen dzieli się na **głowę** (head) i **ogon** (tail).
- Głowa zawiera funkcje i terminale; ogon — wyłącznie terminale.
- Jeśli głowa ma długość $h$, a maksymalna arność funkcji to $n_{\max}$, to ogon ma długość $t=h(n_{\max}-1)+1$ (gwarantuje poprawne drzewo).
- Symbole funkcji: np. $A=\text{AND}$, $O=\text{OR}$, $N=\text{NOT}$; terminale: $a,b,c,\dots$

## 8.3. Dekodowanie (czytanie drzewa wszerz)
1. Pierwszy symbol = korzeń.
2. Czytaj poziomami: każdemu węzłowi-funkcji przypisz tyle kolejnych symboli, ile wynosi jego **arność** (AND/OR: 2, NOT: 1).
3. Kontynuuj aż wszystkie liście są terminalami. Nadmiarowe symbole na końcu genu są ignorowane.

**Przykład:** `OANabc...` → korzeń `O`(2) → dzieci `A`,`N`; `A`(2) → `a`,`b`; `N`(1) → `c`. Wynik: $(a\wedge b)\vee\lnot c$.

## 8.4. Łączenie genów
Wiele genów łączy się ustalonym operatorem (linking function), np. OR:
$$\text{chromosom}=\text{gen}_1\ \text{OR}\ \text{gen}_2.$$

## 8.5. Funkcja dopasowania (fitness) dla funkcji logicznej
1. Zdekoduj i połącz geny → wyrażenie $g$.
2. Zbuduj tablicę prawdy $g$ dla wszystkich $2^n$ kombinacji.
3. Porównaj z funkcją docelową $f$.
4. **Dopasowanie = dokładność** = (liczba zgodnych wierszy)/$2^n$.

## 8.6. Przepis na zadanie
- Ostrożnie zdekoduj każdy gen wszerz (najczęstszy błąd to czytanie „w głąb").
- Połącz operatorem podanym w treści.
- Tabela prawdy obu funkcji, policz zgodności.

## Powiązane zadania
- [Zadanie 1F — fitness = 5/8 = 62.5%](../rozwiazania/zad_1F_gep.md)
