# 📊 Analyse de Données Foncières pour Investisseur Immobilier

## 📋 Description du Projet

Ce projet analyse les données foncières (DVF - Demandes de Valeurs Foncières) et les données de loyers pour les régions **Nouvelle-Aquitaine** et **Occitanie** afin d'identifier les meilleures opportunités d'investissement immobilier en termes de rentabilité.

Le projet comprend 3 notebooks Jupyter qui doivent être exécutés **dans l'ordre** :

| # | Notebook | Description |
|---|----------|-------------|
| 1 | `01_preparation_donnees.ipynb` | Chargement, nettoyage et fusion des données |
| 2 | `02_exploration_analyses.ipynb` | Visualisations et analyses statistiques |
| 3 | `03_application_investisseur.ipynb` | Recommandations pour investisseurs |

---

## 📁 Structure des Données Requises

### 1. Données DVF (Mutations Immobilières)

**Emplacement requis :** 
- `Nouvelle-Aquitaine/` - pour les départements de Nouvelle-Aquitaine
- `Occitanie/` - pour les départements d'Occitanie

**Format des fichiers :** `mutations_dXX.csv` (où XX = numéro du département)

**Colonnes requises dans les CSVs DVF :**

| Colonne | Description | Type |
|---------|-------------|------|
| `idmutation` | Identifiant unique de la mutation | String |
| `datemut` | Date de la mutation | Date |
| `anneemut` | Année de la mutation | Integer |
| `moismut` | Mois de la mutation | Integer |
| `coddep` | Code du département | String/Category |
| `l_codinsee` | Liste des codes INSEE des communes | String |
| `valeurfonc` | Valeur foncière (prix de vente en €) | Float |
| `sbati` | Surface bâtie en m² | Float |
| `libtypbien` | Type de bien (MAISON, APPARTEMENT, etc.) | String/Category |
| `vefa` | Indicateur VEFA (Vente en l'État Futur d'Achèvement) | Category |

**📌 Où obtenir les données DVF ?**
- Site officiel : [data.gouv.fr - DVF](https://www.data.gouv.fr/fr/datasets/demandes-de-valeurs-foncieres/)
- Télécharger les fichiers pour les départements souhaités des régions Nouvelle-Aquitaine et Occitanie

---

### 2. Données de Loyers

**Emplacement requis :** `Loyer/loyers_filtre_occitanie_nouvelle_aquitaine.csv`

**Colonnes requises :**

| Colonne | Description | Type |
|---------|-------------|------|
| `INSEE_C` | Code INSEE de la commune (5 chiffres) | String |
| `DEP` | Code du département | String |
| `REG` | Code de la région | Integer |
| `LIBGEO` | Nom de la commune | String/Category |
| `loypredm2` | Loyer prédit au m² (€/m²/mois) | Float |

**📌 Où obtenir les données de loyers ?**
- Observatoires des loyers locaux
- [Clameur](https://www.clameur.fr/) (observatoire privé des loyers)

---

## 📸 Captures d'Écran à Fournir pour un Bon Rendu

Pour avoir un CSV de qualité et un README complet, voici les captures d'écran recommandées lors de l'exécution des notebooks :

### Notebook 01 - Préparation des Données

| # | Capture d'écran | Description |
|---|-----------------|-------------|
| 1 | **Aperçu des loyers** | Première cellule montrant `loyers.head()` avec les colonnes INSEE_C, DEP, REG, LIBGEO, loypredm2 |
| 2 | **Résumé du traitement** | Le tableau final montrant par département : rows_dvf_clean, rows_merge, communes_couvertes, prix_m2_moy, loyer_m2_moy, rentabilite_m2_moy |

### Notebook 02 - Exploration et Analyses

| # | Capture d'écran | Description |
|---|-----------------|-------------|
| 3 | **Statistiques descriptives** | Output de `communes_all.describe()` montrant les stats pour nb_ventes, prix_m2_moy, loyer_m2_moy, rentabilite_m2_moy |
| 4 | **Histogramme prix au m²** | Graphique "Distribution des prix moyens au m² (communes)" |
| 5 | **Histogramme loyers au m²** | Graphique "Distribution des loyers moyens au m² (communes)" |
| 6 | **Histogramme rentabilité** | Graphique "Distribution des rentabilités brutes moyennes (%) (communes)" |
| 7 | **Prix vs Loyers par département** | Graphique comparatif par département |
| 8 | **Rentabilité par département** | Graphique bar "Rentabilité brute moyenne (%) par département" |

### Notebook 03 - Application Investisseur

| # | Capture d'écran | Description |
|---|-----------------|-------------|
| 9 | **Top 20 communes** | Tableau des 20 communes les plus intéressantes avec score_interet |
| 10 | **Visualisations finales** | Graphiques de recommandation pour l'investisseur |

---

## 🚀 Instructions d'Exécution

```bash
# 1. Installer les dépendances
pip install pandas numpy matplotlib

# 2. Placer les données dans les dossiers appropriés
#    - Nouvelle-Aquitaine/*.csv
#    - Occitanie/*.csv  
#    - Loyer/loyers_filtre_occitanie_nouvelle_aquitaine.csv

# 3. Exécuter les notebooks dans l'ordre
jupyter notebook 01_preparation_donnees.ipynb
jupyter notebook 02_exploration_analyses.ipynb
jupyter notebook 03_application_investisseur.ipynb
```

---

## 📊 Fichiers de Sortie (outputs/clean/)

Après exécution du notebook 01, les fichiers suivants sont générés :

| Type de fichier | Format | Description |
|-----------------|--------|-------------|
| `dvf_dep_XX.csv` | Par département | Données DVF nettoyées |
| `fusion_dep_XX.csv` | Par département | DVF + Loyers fusionnés avec rentabilité |
| `communes_dep_XX.csv` | Par département | Agrégation par commune |
| `communes_all.csv` | **Fichier principal** | Toutes les communes avec nb_ventes, prix_m2_moy, loyer_m2_moy, rentabilite_m2_moy |

---

## 📈 Métriques Calculées

- **prix_m2** : Prix au m² = valeurfonc / sbati
- **rentabilite_m2** : Rentabilité brute (%) = (loypredm2 × 12 × sbati / valeurfonc) × 100
- **score_interet** : Score combinant rentabilité et fiabilité (nombre de ventes)

---

## 🗺️ Couverture Géographique

### Nouvelle-Aquitaine (12 départements)
16, 17, 19, 23, 24, 33, 40, 47, 64, 79, 86, 87

### Occitanie (13 départements)  
09, 11, 12, 30, 31, 32, 34, 46, 48, 65, 66, 81, 82

---

## ⚠️ Notes Importantes

1. **Filtrage des données** : Seules les transactions MAISON/APPARTEMENT > 50 000€ avec surface > 20m² sont conservées
2. **Format loyers** : Si le fichier de loyers utilise le séparateur `;` et la virgule décimale, cela sera géré automatiquement
3. **Mémoire** : Le traitement peut nécessiter plusieurs Go de RAM pour les gros départements (33, 34, etc.)

---

## 📧 Contact

Pour toute question concernant ce projet d'analyse de données foncières, veuillez consulter les notebooks pour plus de détails sur la méthodologie.
