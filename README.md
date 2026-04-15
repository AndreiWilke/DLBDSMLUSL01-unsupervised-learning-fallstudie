# Fallstudie 1 – DLBDSMLUSL01_D

**Psychische Gesundheit in technologiebezogenen Berufen**
Kurs: Maschinelles Lernen – Unsupervised Learning und Feature Engineering
Verfasser: Andrei Wilke | Matrikelnummer: IU14128673
Stand: 15.04.2026 (technische Endfassung des Notebooks)

Dieses Repository enthält den technischen Projektkern: Hauptnotebook, Rohdaten, reproduzierbare Ergebnistabellen und Abbildungen. Der schriftliche Fallstudienbericht wird auf Basis dieses Notebook-Stands in einem separaten Arbeitsschritt als `.docx` / `.pdf` erstellt und ergänzt.

---

## Projektstruktur

```
├── notebooks/
│   └── fallstudie1_main.ipynb                        ← Hauptnotebook (vollständig ausgeführt)
├── reports/
│   ├── figures/                                      ← exportierte Abbildungen (PNG)
│   │   ├── method_comparison_overview.png
│   │   ├── method_silhouette_k2_k4.png
│   │   └── pca_cluster_final.png
│   └── tables/                                       ← exportierte Ergebnistabellen (CSV)
│       ├── 01_sichtungsprotokoll.csv
│       ├── 02_decision_df.csv
│       ├── 03_method_eval.csv
│       ├── 04_cluster_sizes_k2.csv
│       ├── 05_cluster_sizes_k3.csv
│       ├── 06_cluster_profile_k2.csv
│       ├── 07_cluster_profile_k3.csv
│       ├── 08_cluster_diff_k2.csv
│       ├── 09_pca_explained_variance.csv
│       ├── 10_profile_variables_k2_distribution.csv
│       ├── 11_hr_actions_by_cluster.csv
│       ├── 12_medoids_k2.csv
│       └── 13_pam_stability_k2.csv
├── data/
│   └── raw/
│       └── mental_health_tech_2016.csv               ← Rohdaten (OSMI 2016, 1.433 × 63)
├── artifacts/
│   └── checkpoints/                                  ← Notebook-Checkpoints (nicht prüfungsrelevant)
├── .gitignore
└── README.md
```

---

## Methodischer Stand

Das Notebook vergleicht drei Clusterverfahren auf demselben Merkmalsraum (25 gemischte Features: stetig, ordinal, binär) jeweils über k = 2 bis 8 und wählt die finale Lösung daraus aus:

1. **k-Means (euklidisch, StandardScaler)** – Baseline.
2. **PAM / FasterPAM auf Gower-Distanz** – passendes Verfahren für gemischte Merkmalstypen.
3. **Hierarchisches Clustering (average-link) auf Gower-Distanz** – robuste Zweitmeinung.

Finale Wahl: **PAM / FasterPAM auf Gower-Distanz mit k = 2.**
- Silhouette 0,358 (distanzkonsistent auf Gower), gegenüber 0,203 im k-Means-Baseline.
- Konsistentes Optimum bei k = 2 über alle drei Verfahren.
- Stabil über fünf Seeds (identische Silhouette, identische Clustergrößen bis auf Labeltausch).
- Clustergrößen: Cluster 0 = 843 (belastet), Cluster 1 = 590 (gering betroffen).
- Medoids sind reale Befragte und im Bericht zitierbar.

---

## Reproduzierbarer Lauf

### Voraussetzungen

```bash
pip install pandas numpy scikit-learn matplotlib seaborn joblib gower kmedoids scipy
```

### Notebook ausführen

Das Notebook ist self-contained und löst Pfade automatisch auf. Die Ordnerstruktur (`data/raw/`, `reports/`) muss erhalten bleiben.

```bash
cd notebooks/
jupyter nbconvert --to notebook --execute --inplace fallstudie1_main.ipynb
```

Alternativ: Notebook in Jupyter von oben nach unten ausführen.

---

## Erwartete Outputs

**Tabellen** (`reports/tables/`):
- `01_sichtungsprotokoll.csv` – EDA-Sichtungsprotokoll aller 63 Variablen
- `02_decision_df.csv` – Entscheidungsklassen (A/B/C/D) für alle Variablen
- `03_method_eval.csv` – Gütekriterien für k-Means, PAM/Gower, HAC/Gower über k=2..8
- `04_cluster_sizes_k2.csv` / `05_cluster_sizes_k3.csv` – Clustergrößen
- `06_cluster_profile_k2.csv` / `07_cluster_profile_k3.csv` – Clusterprofile
- `08_cluster_diff_k2.csv` – Stärkste Trennmerkmale (PAM k=2)
- `09_pca_explained_variance.csv` – Erklärte Varianzanteile PC1 und PC2
- `10_profile_variables_k2_distribution.csv` – Profilierungsvariablen je Cluster
- `11_hr_actions_by_cluster.csv` – Abgeleitete HR-Maßnahmen
- `12_medoids_k2.csv` – Medoid-Merkmalswerte (reale Befragte als Clusterzentren)
- `13_pam_stability_k2.csv` – Stabilitätscheck PAM/Gower k=2 über fünf Seeds

**Abbildungen** (`reports/figures/`):
- `method_comparison_overview.png` – vier Gütekennzahlen für alle drei Verfahren über k=2..8
- `method_silhouette_k2_k4.png` – Silhouette-Vergleich der Verfahren bei k=2..4
- `pca_cluster_final.png` – PCA-Scatter mit PAM/Gower k=2 (inkl. markierter Medoids), PAM k=3 und k-Means-Baseline als Vergleichspanel

---

## Datenquelle

- Kaggle / OSMI: **Mental Health in Tech Survey 2016**
- URL: <https://www.kaggle.com/osmi/mental-health-in-tech-2016>
- Datei: `data/raw/mental_health_tech_2016.csv` (1.433 Zeilen, 63 Spalten)
