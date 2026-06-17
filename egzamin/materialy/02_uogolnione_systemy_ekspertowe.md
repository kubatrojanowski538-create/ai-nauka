# 2. Uogólnione (relacyjne) rozmyte systemy ekspertowe

Te systemy realizują wnioskowanie **rozmyte oparte na relacjach** (kompozycja sup-T), z regułami zapisanymi jako implikacje rozmyte. Stosowane operatory to zwykle operatory **Łukasiewicza / ograniczone**.

## 2.1. Operatory logiki rozmytej (Łukasiewicz)
| operacja | wzór |
|---|---|
| implikacja $a\to b$ | $\min(1,\,1-a+b)$ |
| OR (suma ograniczona) $a\oplus b$ | $\min(1,\,a+b)$ |
| AND (iloczyn ograniczony) $a\otimes b$ | $\max(0,\,a+b-1)$ |
| łączenie reguł $\wedge$ | $\max(0,\,a+b-1)$ (jak AND) |
| negacja $\lnot a$ | $1-a$ |
| min/max | $\wedge=\min$, $\vee=\max$ (gdy tak zdefiniowano) |

> Uwaga na słowny opis reguł: „**nie** są drogie" oznacza $\lnot D=1-D$; „szybkie **i** nie drogie" = $S\otimes\lnot D$; „niezawodne **lub** z gwarancją" = $N\oplus G$.

## 2.2. Procedura wnioskowania (4 kroki)
Dane: zbiory rozmyte na wejściu $X$, zbiory (zwykłe) na wyjściu $Y$ ($Q_k$), reguły $R_k$, wektor obserwacji $A'(x)$.

**Krok 1 — relacje cząstkowe i globalna.**
Dla każdej reguły $R_k$: poprzednik $A_k(x)$ (wynik operatorów na zbiorach wejściowych), a relacja:
$$R_k(x,y)=A_k(x)\to Q_k(y)=\min\big(1,\,1-A_k(x)+Q_k(y)\big).$$
Relacja globalna (łączenie reguł iloczynem ograniczonym):
$$R(x,y)=R_1(x,y)\otimes R_2(x,y)\otimes\cdots=\max\big(0,\textstyle\sum_k R_k(x,y)-(L-1)\big)$$
(dla $L$ reguł; w praktyce składamy parami $\max(0,a+b-1)$).

**Krok 2 — rozmywanie wejścia.** Zadany wektor preferencji/obserwacji $A'(x)$.

**Krok 3 — wnioskowanie (kompozycja sup-⊗):**
$$B'(y)=\sup_{x\in X}\big[A'(x)\otimes R(x,y)\big]=\max_x \max\big(0,\,A'(x)+R(x,y)-1\big).$$

**Krok 4 — wyostrzanie (środek ciężkości):**
$$y^\*=\frac{\sum_j y_j\,B'(y_j)}{\sum_j B'(y_j)}.$$
Gdy wyjście to „nominalna liczba × stopień" (np. liczba pracowników na zmianę), wyostrzamy **racjonalnie**: $\text{wynik}_j=y_j\cdot B'(y_j)$.

## 2.3. Macierzowo
- $A_k$, $Q_k$ to wektory; $R_k$ to macierz $|X|\times|Y|$ liczona „każdy z każdym" wzorem implikacji.
- $\otimes$ między macierzami = element po elemencie.
- $B'(y_j)=\max_i \max(0, A'(x_i)+R(x_i,y_j)-1)$.

## 2.4. Najczęstsze błędy
- Pominięcie negacji w „nie drogie".
- Mylenie kierunku implikacji ($A\to Q$, nie $Q\to A$).
- Niewłaściwe łączenie reguł (musi być $\otimes$, nie min).
- Zła kolejność: najpierw poprzedniki → relacje → globalna → wnioskowanie → wyostrzanie.

## Powiązane zadania
- [1B (zdj.3) — komputery, $A'=[0.7,0.1,0.2]$](../rozwiazania/zad_1B_system_ekspertowy_komputery.md)
- [zdj.14 — komputery, $A'=[0.4,0.5,0.8]$](../rozwiazania/zad_1_zdj14_system_ekspertowy_komputery.md)
- [zdj.19 — komputery, $A'=[0,0.8,0.2]$](../rozwiazania/zad_1A_zdj19_komputery.md)
- [zdj.8 — budynek, 3 wyjścia](../rozwiazania/zad_1A_zdj8_budynek_acc07.md)
- [zdj.15 — budynek, 3 wyjścia](../rozwiazania/zad_1A_zdj15_budynek_acc05.md)
