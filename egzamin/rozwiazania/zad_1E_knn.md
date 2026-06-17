# Zadanie 1E (grupa E) — Klasyfikacja metodą kNN

## Treść (skrót)
Punkty z klasami ($\circ$, $\ast$):

| pkt | $(x_1,x_2)$ | klasa |
|---|---|---|
| A | (1,2) | $\circ$ |
| B | (2,3) | $\circ$ |
| C | (3,1) | $\circ$ |
| D | (6,5) | $\ast$ |
| E | (7,7) | $\ast$ |
| F | (8,6) | $\ast$ |
| G | (1,0) | $\circ$ |
| H | (6,4) | $\ast$ |

Dla $k=3$ wyznaczyć klasę punktu $P=(4,3)$.

## Krok 1 — odległości euklidesowe do $P=(4,3)$
$$d=\sqrt{(x_1-4)^2+(x_2-3)^2}$$

| pkt | $(x_1-4)^2+(x_2-3)^2$ | $d$ | klasa |
|---|---|---|---|
| A (1,2) | $9+1=10$ | $3.16$ | $\circ$ |
| **B (2,3)** | $4+0=4$ | $\mathbf{2.00}$ | $\circ$ |
| **C (3,1)** | $1+4=5$ | $\mathbf{2.24}$ | $\circ$ |
| D (6,5) | $4+4=8$ | $2.83$ | $\ast$ |
| E (7,7) | $9+16=25$ | $5.00$ | $\ast$ |
| F (8,6) | $16+9=25$ | $5.00$ | $\ast$ |
| G (1,0) | $9+9=18$ | $4.24$ | $\circ$ |
| **H (6,4)** | $4+1=5$ | $\mathbf{2.24}$ | $\ast$ |

## Krok 2 — wybór 3 najbliższych sąsiadów
Posortowane rosnąco: $B\ (2.00) < C\ (2.24) = H\ (2.24) < D\ (2.83)<\dots$

Trzej najbliżsi sąsiedzi: **B ($\circ$), C ($\circ$), H ($\ast$)**.

(C i H mają jednakową odległość $\sqrt5$; oba są bliższe niż następny punkt D, więc oba wchodzą do trójki.)

## Krok 3 — głosowanie większościowe
- klasa $\circ$: 2 głosy (B, C)
- klasa $\ast$: 1 głos (H)

$$\boxed{\,P=(4,3)\ \text{należy do klasy}\ \circ\,}$$

Mimo bliskości punktu H ($\ast$), przewaga dwóch sąsiadów klasy $\circ$ przesądza o przypisaniu $P$ do klasy $\circ$.
