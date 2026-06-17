# Zadanie 2E (grupa E) — Sieć probabilistyczna PNN

## Treść (skrót)
Trzy klasy ($K=3$):
- Klasa 1: $x_1=(1,-1),\ x_2=(0,2)$
- Klasa 2: $x_3=(-3,3),\ x_4=(4,5),\ x_5=(-2,2)$
- Klasa 3: $x_6=(1,0),\ x_7=(2,2)$

Każdy neuron wzorcowy ma gaussowskie jądro o $\sigma_i=1/\sqrt2$:
$$K(x,x_i)=\exp\!\Big(-\frac{\lVert x-x_i\rVert^2}{2\sigma_i^2}\Big).$$
Sieć liczy średnią odpowiedzi w klasie: $g_k(x)=\frac1{n_k}\sum_{i\in C_k}K(x,x_i)$, decyzja $\text{class}(x)=\arg\max_k g_k(x)$.

## Krok 0 — uproszczenie jądra
$2\sigma_i^2=2\cdot\tfrac12=1$, więc
$$K(x,x_i)=\exp\big(-\lVert x-x_i\rVert^2\big).$$

## Architektura sieci PNN (4 warstwy)
1. **Warstwa wejściowa** — podaje współrzędne $x=(x_1,x_2)$ na wszystkie neurony.
2. **Warstwa wzorcowa** — po jednym neuronie na wzorzec ($Q=7$ neuronów); neuron $i$ liczy $K(x,x_i)=\exp(-\lVert x-x_i\rVert^2)$.
3. **Warstwa sumacyjna** — po jednym neuronie na klasę; uśrednia odpowiedzi wzorców danej klasy: $g_k(x)=\frac1{n_k}\sum_{i\in C_k}K(x,x_i)$, gdzie $n_1=2,\ n_2=3,\ n_3=2$.
4. **Warstwa decyzyjna** — wybiera klasę o największym $g_k(x)$.

## Krok po kroku — wzory dla dowolnego punktu testowego $x=(x_1,x_2)$
$$g_1(x)=\tfrac12\Big[e^{-((x_1-1)^2+(x_2+1)^2)}+e^{-(x_1^2+(x_2-2)^2)}\Big]$$
$$g_2(x)=\tfrac13\Big[e^{-((x_1+3)^2+(x_2-3)^2)}+e^{-((x_1-4)^2+(x_2-5)^2)}+e^{-((x_1+2)^2+(x_2-2)^2)}\Big]$$
$$g_3(x)=\tfrac12\Big[e^{-((x_1-1)^2+x_2^2)}+e^{-((x_1-2)^2+(x_2-2)^2)}\Big]$$
$$\text{class}(x)=\arg\max_{k\in\{1,2,3\}} g_k(x).$$

## Przykład liczbowy — punkt testowy $x=(1,1)$
**Warstwa wzorcowa** (odległości$^2$ i jądra):

| wzorzec | $\lVert x-x_i\rVert^2$ | $K=e^{-\lVert\cdot\rVert^2}$ | klasa |
|---|---|---|---|
| $x_1=(1,-1)$ | $0+4=4$ | $0.0183$ | 1 |
| $x_2=(0,2)$ | $1+1=2$ | $0.1353$ | 1 |
| $x_3=(-3,3)$ | $16+4=20$ | $2.1\cdot10^{-9}$ | 2 |
| $x_4=(4,5)$ | $9+16=25$ | $1.4\cdot10^{-11}$ | 2 |
| $x_5=(-2,2)$ | $9+1=10$ | $4.5\cdot10^{-5}$ | 2 |
| $x_6=(1,0)$ | $0+1=1$ | $0.3679$ | 3 |
| $x_7=(2,2)$ | $1+1=2$ | $0.1353$ | 3 |

**Warstwa sumacyjna:**
$$g_1=\tfrac12(0.0183+0.1353)=0.0768,$$
$$g_2=\tfrac13(2.1\cdot10^{-9}+1.4\cdot10^{-11}+4.5\cdot10^{-5})\approx1.5\cdot10^{-5},$$
$$g_3=\tfrac12(0.3679+0.1353)=0.2516.$$

**Warstwa decyzyjna:** $\max\{0.0768,\ 1.5\cdot10^{-5},\ 0.2516\}=g_3$.

$$\boxed{\,\text{class}(1,1)=\text{klasa 3}\,}$$

Decyzja jest zdominowana przez najbliższe wzorce ($x_6$ i $x_7$ z klasy 3), co jest istotą PNN — jądra gaussowskie nadają największą wagę wzorcom leżącym najbliżej punktu testowego.
