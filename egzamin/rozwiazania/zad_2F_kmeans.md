# Zadanie 2F (grupa F) — Algorytm k-średnich (k-means)

## Treść (skrót)
Punkty: $(1,4),(2,3),(7,7),(8,6)$, $k=2$. Centra początkowe: $c_1=(1,4)$, $c_2=(2,3)$.

Stosujemy kwadrat odległości euklidesowej $d^2$ (monotoniczny, wystarcza do przypisania).

## Iteracja 1
Centra: $c_1=(1,4)$, $c_2=(2,3)$.

| punkt | $d^2$ do $c_1$ | $d^2$ do $c_2$ | przypisanie |
|---|---|---|---|
| $(1,4)$ | 0 | 2 | $C_1$ |
| $(2,3)$ | 2 | 0 | $C_2$ |
| $(7,7)$ | 45 | 41 | $C_2$ |
| $(8,6)$ | 53 | 45 | $C_2$ |

Klastry: $C_1=\{(1,4)\}$, $C_2=\{(2,3),(7,7),(8,6)\}$.

Nowe centra:
$$c_1=(1,4),\qquad c_2=\Big(\tfrac{2+7+8}{3},\tfrac{3+7+6}{3}\Big)=\big(\tfrac{17}{3},\tfrac{16}{3}\big)\approx(5.67,\,5.33).$$

## Iteracja 2
Centra: $c_1=(1,4)$, $c_2\approx(5.67,5.33)$.

| punkt | $d^2$ do $c_1$ | $d^2$ do $c_2$ | przypisanie |
|---|---|---|---|
| $(1,4)$ | 0 | 23.6 | $C_1$ |
| $(2,3)$ | 2 | 18.9 | $C_1$ |
| $(7,7)$ | 45 | 4.6 | $C_2$ |
| $(8,6)$ | 53 | 5.9 | $C_2$ |

Klastry: $C_1=\{(1,4),(2,3)\}$, $C_2=\{(7,7),(8,6)\}$.

Nowe centra:
$$c_1=\big(\tfrac{1+2}{2},\tfrac{4+3}{2}\big)=(1.5,\,3.5),\qquad c_2=\big(\tfrac{7+8}{2},\tfrac{7+6}{2}\big)=(7.5,\,6.5).$$

## Iteracja 3 (sprawdzenie zbieżności)
Centra: $c_1=(1.5,3.5)$, $c_2=(7.5,6.5)$.

| punkt | $d^2$ do $c_1$ | $d^2$ do $c_2$ | przypisanie |
|---|---|---|---|
| $(1,4)$ | 0.5 | duże | $C_1$ |
| $(2,3)$ | 0.5 | duże | $C_1$ |
| $(7,7)$ | duże | 0.5 | $C_2$ |
| $(8,6)$ | duże | 0.5 | $C_2$ |

Przypisania **bez zmian** → algorytm zbiegł.

## Wynik końcowy
$$\boxed{\,C_1=\{(1,4),(2,3)\},\ c_1=(1.5,\,3.5);\qquad C_2=\{(7,7),(8,6)\},\ c_2=(7.5,\,6.5)\,}$$

Algorytm rozdzielił punkty na dwie naturalne grupy: „lewy dolny" i „prawy górny" róg.
