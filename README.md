# Approximation Algorithms for Steiner Trees in Weighted Graphs

## Opis projekta

Projekat za kurs **Naučno izračunavanje 2025/26** na Matematičkom fakultetu, Univerzitet u Beogradu.

Tema je implementacija i poređenje aproksimacionih algoritama za problem Steinerovog stabla u težinskim grafovima. Steinerov problem je NP-težak: cilj je pronaći stablo minimalne težine koje povezuje zadati skup terminala u grafu, koristeći po potrebi i neterminalne čvorove.

## Algoritmi

1. **Brute Force** — egzaktan, enumeracija svih podskupova neterminalnih čvorova. Primenljiv samo na male grafove (~30 čvorova).
2. **MST Heuristika** (Kou, Markowsky, Berman, 1981) — aproksimacioni faktor 2. Gradi kompletni graf najkraćih puteva između terminala pa traži MST.
3. **Mehlhorn** (1988) — aproksimacioni faktor 2. Koristi Voronoi particiju grafa za brzu konstrukciju.
4. **SPH** (Takahashi, Matsuyama, 1980) — aproksimacioni faktor 2. Greedy dodavanje najbližeg terminala.
5. **Zelikovsky** (1993) — aproksimacioni faktor 11/6 ≈ 1.83. Poboljšava početno rešenje koristeći trojke terminala i Steinerove tačke.
6. **Zelikovsky + SPH baza** — Zelikovsky sa SPH umesto MST heuristike kao početnim rešenjem.
7. **Zelikovsky + Mehlhorn baza** — Zelikovsky sa Mehlhorn-om kao početnim rešenjem.

## Skupovi podataka

Korišćeni su benchmark setovi iz [SteinLib](http://steinlib.zib.de/) kolekcije:

- **small** (small01–small10) — 5 do 30 čvorova, za verifikaciju sa brute force-om
- **B** (b01–b18, J. E. Beasley) — 50 do 100 čvorova, 9 do 50 terminala
- **C** (c01–c20) — 500 čvorova, do 100 terminala
  - **C_30_terminals** — redukovana verzija sa max 30 terminala
  - **C_50_terminals** — redukovana verzija sa max 50 terminala

Format fajlova: STP (Steiner Tree Problem format).

## Struktura projekta

```
├── 01_algorithms.ipynb                 # Implementacije svih algoritama + STP parser
├── 02_evaluation_and_visualization.ipynb  # Pomoćne funkcije za testiranje i vizuelizaciju
├── 03_test_small.ipynb                 # Testovi na small setu (sa brute force-om)
├── 04_test_B.ipynb                     # Testovi na B setu
├── 05_test_C_30_terminals.ipynb        # Testovi na C setu (max 30 terminala)
├── 06_test_C_50_terminals.ipynb        # Testovi na C setu (max 50 terminala)
├── 07_final_conclusions.ipynb          # Konačni zaključci i poređenje svih rezultata
├── 08_presentation.ipynb               # Prezentacija za odbranu projekta
├── data/
│   ├── B/                              # SteinLib B benchmark (b01–b18)
│   ├── C/                              # SteinLib C benchmark (c01–c20)
│   ├── C_30_terminals/                 # C sa max 30 terminala
│   ├── C_50_terminals/                 # C sa max 50 terminala
│   └── small/                          # Mali test primeri (small01–small10)
├── requirements.txt
└── README.md
```

## Pokretanje

```bash
python -m venv .venv
.venv\Scripts\activate        # Windows
# source .venv/bin/activate   # Linux/macOS
pip install -r requirements.txt
jupyter notebook
```

Notebookovi se pokreću redom: prvo `01_algorithms`, pa `02_evaluation_and_visualization` (učitava 01), pa `03`/`04`/`05`/`06` (svaki učitava 02). Finalni zaključci su u `07_final_conclusions`.

## Napomene

Zelikovsky algoritam ima bolji teorijski faktor (11/6 vs 2), ali zbog složenosti O(t³·n) postaje nepraktičan na grafovima sa više od ~100 čvorova i većim brojem terminala. Na B setu (do 100 čvorova) radi za par minuta po instanci, dok na većim grafovima može trajati satima.

## Literatura

### Predavanje (osnova)

- Dinitz, M. (2026). [*Lecture 2: Steiner Tree, TSP.*](https://www.cs.jhu.edu/~mdinitz/classes/ApproxAlgorithms/Spring2026/Lectures/Lecture2/lecture2.pdf) 601.435/635 Approximation Algorithms, Johns Hopkins University.

### MST heuristika / Kou–Markowsky–Berman

- Pajor, T., Uchoa, E., & Werneck, R. F. (2018). [*Strong Steiner Tree Approximations in Practice.*](https://arxiv.org/pdf/1409.8318)

### Mehlhorn (Voronoi-based ubrzanje)

- Mehlhorn, K. (1988). [*A faster approximation algorithm for the Steiner problem in graphs.*](https://doi.org/10.1016/0020-0190(88)90066-X) Information Processing Letters, 27(3), 125–128.
- Bampis, E. et al. (2024). [*Approximation Algorithms for Combinatorial Optimization with Predictions*](https://arxiv.org/pdf/2411.16600) (sadrži detaljnu rekonstrukciju Mehlhornovog algoritma, Sec. 4).

### Shortest Path Heuristic (SPH) / Takahashi–Matsuyama

- Huang, S. Y. et al. (2013). [*Steiner tree methods for optimal sub-network identification: an empirical study.*](https://link.springer.com/article/10.1186/1471-2105-14-144) BMC Bioinformatics, 14, 144.

### Zelikovsky (11/6-aproksimacija)

- Zelikovsky, A. Z. (1993). [*An 11/6-approximation algorithm for the network Steiner problem.*](https://www.researchgate.net/publication/226738451_An_116-approximation_algorithm_for_the_network_Steiner_problem) Algorithmica, 9(5), 463–470.

## Autor

**Nikola Labus** — Matematički fakultet, Univerzitet u Beogradu
