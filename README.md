# Fallstudie 1 – DLBDSMLUSL01_D

**Thema:** Psychische Gesundheit in technologiebezogenen Berufen  
**Kurs:** Maschinelles Lernen – Unsupervised Learning und Feature Engineering  
**Verfasser:** Andrei Wilke  
**Matrikelnummer:** IU14128673  
**Stand:** 15.04.2026

Dieses Repository enthält den reproduzierbaren technischen Projektkern der Fallstudie:
- Hauptnotebook
- Rohdatensatz

Der schriftliche Fallstudienbericht wird separat eingereicht und ist nicht Teil des versionierten Repositories.

## Versionierte Struktur

- notebooks/fallstudie1_main.ipynb
- data/raw/mental_health_tech_2016.csv
- .gitignore
- README.md

## Lokal erzeugte Ordner

Beim Ausführen des Notebooks werden lokal erzeugt:
- reports/tables/
- reports/figures/
- artifacts/checkpoints/

Diese Verzeichnisse sind nicht Teil des versionierten Git-Stands.

## Reproduzierbarer Lauf

Voraussetzungen:
- pandas
- numpy
- scikit-learn
- matplotlib
- seaborn
- joblib
- gower
- kmedoids
- scipy

Notebook ausführen:
- in den Ordner notebooks wechseln
- fallstudie1_main.ipynb vollständig von oben nach unten ausführen
- alternativ per nbconvert ausführen

## Methodischer Kern

Im Notebook werden drei Verfahren auf demselben Merkmalsraum verglichen:
1. k-Means als Baseline
2. PAM / FasterPAM auf Gower-Distanz
3. Hierarchisches Clustering auf Gower-Distanz

Finale Modellwahl:
PAM / FasterPAM auf Gower-Distanz mit k = 2

## Datenquelle

- Kaggle / OSMI
- Mental Health in Tech Survey 2016
- Datei: data/raw/mental_health_tech_2016.csv
