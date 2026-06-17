# Zadanie 2B (zdjęcie 11) — System TSK odwzorowujący funkcję 2 zmiennych

## Treść (skrót)
System TSK idealnie odwzorowuje
$$S(x_1,x_2)=1+x_1-x_2+5x_1x_2,$$
gdzie $(x_1,x_2)\in[-\alpha_1,\beta_1]\times[-\alpha_2,\beta_2]=[-2,0]\times[0,1]$.
Naszkicować przynależności i podać następniki reguł. Wskazówka: $g=[1,x_1,x_2,x_1x_2]^T$, $q_i=S$ w narożnikach.

## Krok 1 — granice i przynależności
Z dziedziny: $\alpha_1=2,\ \beta_1=0$ (czyli $x_1\in[-2,0]$); $\alpha_2=0,\ \beta_2=1$ (czyli $x_2\in[0,1]$).

Liniowe, komplementarne przynależności $N_k=\dfrac{\beta_k-x_k}{\alpha_k+\beta_k}$:
$$N_1(x_1)=\frac{0-x_1}{2}=-\frac{x_1}{2},\qquad P_1(x_1)=1+\frac{x_1}{2},$$
$$N_2(x_2)=\frac{1-x_2}{1}=1-x_2,\qquad P_2(x_2)=x_2.$$

**Szkic przynależności:**
```
  N1(x1)              P1(x1)            N2(x2)            P2(x2)
1 *                       *         1 *                      *
  | \                  / |            | \                 / |
  |   \              /   |            |   \             /   |
0 |_____*        *_____|             0 |_____*       *_____|
 -2     0        -2    0              0     1        0     1
N1=1 w x1=-2, =0 w x1=0           N2=1 w x2=0, =0 w x2=1
```

## Krok 2 — następniki reguł = wartości $S$ w narożnikach
Cztery reguły odpowiadają kombinacjom $(N_1/P_1,\,N_2/P_2)$. Następniki:
$$q_1=S(-\alpha_1,-\alpha_2)=S(-2,0)=1-2-0+0=-1\quad (N_1,N_2),$$
$$q_2=S(\beta_1,-\alpha_2)=S(0,0)=1+0-0+0=1\quad (P_1,N_2),$$
$$q_3=S(-\alpha_1,\beta_2)=S(-2,1)=1-2-1+5(-2)(1)=-12\quad (N_1,P_2),$$
$$q_4=S(\beta_1,\beta_2)=S(0,1)=1+0-1+0=0\quad (P_1,P_2).$$

$$\boxed{\,q_1=-1,\quad q_2=1,\quad q_3=-12,\quad q_4=0\,}$$

Reguły:
- $R_1$: jeśli $x_1$ jest $N_1$ i $x_2$ jest $N_2$, to $S=-1$
- $R_2$: jeśli $x_1$ jest $P_1$ i $x_2$ jest $N_2$, to $S=1$
- $R_3$: jeśli $x_1$ jest $N_1$ i $x_2$ jest $P_2$, to $S=-12$
- $R_4$: jeśli $x_1$ jest $P_1$ i $x_2$ jest $P_2$, to $S=0$

## Weryfikacja (punkt środkowy $x_1=-1,\ x_2=0.5$)
Przynależności: $N_1=0.5,P_1=0.5,N_2=0.5,P_2=0.5$.
$$S_{TSK}=0.25(-1)+0.25(1)+0.25(-12)+0.25(0)=-3.$$
$$S(-1,0.5)=1-1-0.5+5(-1)(0.5)=-3\ \checkmark$$

Ponieważ $S$ jest funkcją dwuliniową, system TSK z liniowymi przynależnościami i tymi czterema singletonowymi następnikami odtwarza ją **dokładnie** w całej dziedzinie.
