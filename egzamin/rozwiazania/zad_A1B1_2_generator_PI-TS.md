# Zadanie 2 (grupa A1/B1) — Generator systemu PI-TS (4 wejścia)

## Treść (skrót)
System Takagi–Sugeno o 4 wejściach $z_1,\dots,z_4$ z liniowymi, komplementarnymi przynależnościami
$$N_k(z_k)=\frac{\beta_k-z_k}{\alpha_k+\beta_k},\qquad P_k(z_k)=1-N_k(z_k)=\frac{z_k+\alpha_k}{\alpha_k+\beta_k},$$
dla $z_k\in[-\alpha_k,\beta_k]$, $k=1,2,3,4$. Napisać postać **generatora** systemu.

## Rozwiązanie

### Wyjście systemu jako średnia ważona
Przy 4 wejściach, każde z dwoma zbiorami ($N_k$, $P_k$), mamy $2^4=16$ reguł. Wyjście TS:
$$S(z)=\frac{\displaystyle\sum_{i_1,i_2,i_3,i_4\in\{0,1\}} m_{i_1i_2i_3i_4}\,q_{i_1i_2i_3i_4}}{\displaystyle\sum m_{i_1i_2i_3i_4}},$$
gdzie stopień dopasowania jest iloczynem przynależności
$$m_{i_1i_2i_3i_4}=\prod_{k=1}^4 \mu_k^{(i_k)}(z_k),\qquad \mu_k^{(0)}=N_k,\ \mu_k^{(1)}=P_k.$$

### Mianownik = 1
Z komplementarności $N_k+P_k=1$:
$$\sum_{i_1,\dots,i_4} m_{i_1\dots i_4}=\prod_{k=1}^4 (N_k+P_k)=1.$$

### Postać generatora (forma analityczna)
Ponieważ przynależności są **liniowe** w $z_k$, suma ważona jest **funkcją wieloliniową (multiliniową)** — wielomianem zawierającym wszystkie iloczyny podzbiorów zmiennych. Generator (wektor bazowy) ma 16 składowych:
$$g(z)=\big[\,1,\ z_1,z_2,z_3,z_4,\ z_1z_2,z_1z_3,z_1z_4,z_2z_3,z_2z_4,z_3z_4,$$
$$z_1z_2z_3,z_1z_2z_4,z_1z_3z_4,z_2z_3z_4,\ z_1z_2z_3z_4\,\big]^T.$$

Wówczas wyjście systemu zapisujemy w **postaci generatora**:
$$\boxed{\,S(z)=g^T(z)\,(\Omega^T)^{-1}\,q\,}$$
gdzie:
- $q=[q_1,\dots,q_{16}]^T$ — wektor następników 16 reguł (po jednym dla każdego narożnika hiperkostki $[-\alpha_k,\beta_k]$),
- $\Omega$ — macierz $16\times16$ wartości generatora $g$ obliczonych w 16 narożnikach dziedziny (wierzchołkach), tzn. $\Omega_{rs}=g_s(\text{narożnik}_r)$,
- $(\Omega^T)^{-1}q$ — wektor współczynników wielomianu wieloliniowego.

### Postać równoważna
Ze względu na wieloliniowość wystarczy znajomość wartości w narożnikach. Następniki reguł są równe wartościom $S$ w wierzchołkach dziedziny:
$$q_{i_1i_2i_3i_4}=S\big(\zeta_1^{(i_1)},\zeta_2^{(i_2)},\zeta_3^{(i_3)},\zeta_4^{(i_4)}\big),\quad
\zeta_k^{(0)}=-\alpha_k\ (N_k=1),\ \zeta_k^{(1)}=\beta_k\ (P_k=1).$$

To jest „generator" systemu PI-TS: realizuje on dowolną funkcję wieloliniową 4 zmiennych poprzez zadanie 16 wartości w narożnikach i interpolację rozmytymi przynależnościami.
