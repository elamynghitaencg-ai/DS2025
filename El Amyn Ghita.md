# Rapport d'Analyse Approfondie du PIB
## Comparaison Internationale Multi-pays (2015-2023)

El Amyn Ghita
![WhatsApp Image 2025-10-30 à 11 31 39_3660fcba](https://github.com/user-attachments/assets/bf083937-79aa-44a6-85a7-926ecd2e59c0)


## 1. Introduction et Contexte

### 1.1 Objectif de l'analyse

L'objectif principal de cette analyse est d'examiner et de comparer les performances économiques de plusieurs pays à travers l'étude de leur Produit Intérieur Brut (PIB). Cette étude vise à :

- Identifier les tendances de croissance économique sur la période 2015-2023
- Comparer les niveaux de développement économique entre différentes régions du monde
- Analyser la résilience économique face aux chocs mondiaux (notamment la pandémie COVID-19)
- Fournir des insights sur les disparités économiques internationales

### 1.2 Méthodologie générale employée

Notre approche méthodologique repose sur une analyse quantitative combinant :

1. **Analyse descriptive** : calcul de statistiques centrales et de dispersion
2. **Analyse comparative** : benchmarking entre pays et régions
3. **Analyse temporelle** : étude des évolutions et des taux de croissance
4. **Visualisation de données** : représentations graphiques pour faciliter l'interprétation

### 1.3 Pays sélectionnés et période d'analyse

**Pays sélectionnés** (10 pays représentant différentes régions et niveaux de développement) :

- **Amérique du Nord** : États-Unis, Canada
- **Europe** : Allemagne, France, Royaume-Uni
- **Asie** : Chine, Japon, Inde
- **Amérique du Sud** : Brésil
- **Afrique** : Afrique du Sud

**Période d'analyse** : 2015-2023 (9 années)

Cette période permet de capturer les dynamiques pré-pandémie, l'impact de la COVID-19, et la reprise économique post-crise.

### 1.4 Questions de recherche principales

1. Quelles sont les tendances de croissance du PIB pour chaque pays sur la période étudiée ?
2. Comment les différents pays se classent-ils en termes de PIB nominal et de PIB par habitant ?
3. Quel a été l'impact de la pandémie COVID-19 sur les économies analysées ?
4. Quelles corrélations peut-on observer entre les performances économiques des différents pays ?
5. Quelles sont les disparités de développement économique entre pays développés et émergents ?

---

## 2. Description des Données

### 2.1 Source des données

**Source principale** : Banque mondiale - World Development Indicators (WDI)

**Sources complémentaires** :
- Fonds Monétaire International (FMI) - World Economic Outlook Database
- OCDE - Statistics Database

**Fiabilité** : Les données de la Banque mondiale sont considérées comme la référence internationale pour les comparaisons macroéconomiques. Elles sont collectées selon des méthodologies standardisées permettant des comparaisons inter-pays robustes.

### 2.2 Variables analysées

| Variable | Description | Unité | Code WDI |
|----------|-------------|-------|----------|
| **PIB nominal** | Valeur totale de la production de biens et services | Milliards USD courants | NY.GDP.MKTP.CD |
| **PIB par habitant** | PIB divisé par la population | USD courants | NY.GDP.PCAP.CD |
| **Taux de croissance du PIB** | Variation annuelle du PIB en volume | % annuel | NY.GDP.MKTP.KD.ZG |
| **Population** | Nombre d'habitants | Millions | SP.POP.TOTL |

### 2.3 Période couverte

- **Début** : 2015
- **Fin** : 2023
- **Fréquence** : Annuelle
- **Nombre d'observations** : 9 années × 10 pays = 90 observations par variable

### 2.4 Qualité et limites des données

**Points forts** :
- Méthodologie standardisée internationale (System of National Accounts - SNA 2008)
- Couverture temporelle et géographique étendue
- Données régulièrement révisées et mises à jour
- Transparence des méthodes de collecte

**Limites identifiées** :
1. **Délai de publication** : Les données les plus récentes peuvent être provisoires
2. **Comparabilité** : Malgré les standards, des différences méthodologiques nationales persistent
3. **Économie informelle** : Non prise en compte complète dans certains pays émergents
4. **Taux de change** : Les conversions en USD peuvent introduire des distorsions
5. **Données 2023** : Estimations préliminaires susceptibles de révisions

### 2.5 Tableau récapitulatif des données

#### Structure des données collectées

```
Dimensions du dataset :
- 10 pays
- 9 années (2015-2023)
- 4 variables principales
- Total : 360 points de données
```

#### Exemple de structure des données (aperçu)

| Pays | Année | PIB (Mds USD) | PIB/hab (USD) | Croissance (%) | Population (M) |
|------|-------|---------------|---------------|----------------|----------------|
| États-Unis | 2015 | 18,206 | 56,421 | 2.7 | 322.7 |
| États-Unis | 2016 | 18,715 | 57,808 | 1.7 | 323.7 |
| ... | ... | ... | ... | ... | ... |
| Chine | 2015 | 11,061 | 8,033 | 7.0 | 1,376.0 |
| Chine | 2016 | 11,233 | 8,147 | 6.8 | 1,379.0 |

*Note : Les valeurs présentées ci-dessus sont illustratives. Les données réelles seront chargées via l'analyse Python.*

---

## 3. Code d'Analyse

### 3.1 Configuration de l'environnement

#### Importation des bibliothèques nécessaires

**Explication** : Nous commençons par importer toutes les bibliothèques Python nécessaires pour l'analyse de données, les calculs statistiques et la visualisation. Chaque bibliothèque a un rôle spécifique dans notre pipeline d'analyse.

```python
# Importation des bibliothèques pour la manipulation de données
import pandas as pd  # Manipulation et analyse de données tabulaires
import numpy as np   # Calculs numériques et opérations sur tableaux

# Importation des bibliothèques pour la visualisation
import matplotlib.pyplot as plt  # Création de graphiques de base
import seaborn as sns            # Visualisations statistiques avancées

# Configuration de l'affichage des graphiques
plt.style.use('seaborn-v0_8-darkgrid')  # Style professionnel pour les graphiques
sns.set_palette("husl")                  # Palette de couleurs harmonieuse

# Configuration des options d'affichage de pandas
pd.set_option('display.max_columns', None)      # Afficher toutes les colonnes
pd.set_option('display.max_rows', 100)          # Afficher jusqu'à 100 lignes
pd.set_option('display.float_format', '{:.2f}'.format)  # Format des nombres flottants

# Désactivation des avertissements pour un affichage propre
import warnings
warnings.filterwarnings('ignore')

# Confirmation du chargement
print("✓ Bibliothèques importées avec succès")
print(f"✓ Version pandas : {pd.__version__}")
print(f"✓ Version numpy : {np.__version__}")
```

**Résultat attendu** : Toutes les bibliothèques sont maintenant disponibles et configurées pour une analyse optimale.

---

### 3.2 Création du dataset simulé

**Explication** : Comme nous n'avons pas accès direct aux API de la Banque mondiale dans cet environnement, nous créons un dataset réaliste basé sur les tendances économiques réelles observées entre 2015 et 2023. Les données sont calibrées pour refléter les ordres de grandeur et les tendances réelles.

```python
# Définition de la graine aléatoire pour la reproductibilité
np.random.seed(42)

# Définition des pays et des années d'analyse
pays_liste = [
    'États-Unis', 'Chine', 'Japon', 'Allemagne', 'Inde',
    'Royaume-Uni', 'France', 'Brésil', 'Canada', 'Afrique du Sud'
]
annees = list(range(2015, 2024))  # 2015 à 2023 inclus

# Création d'un dictionnaire pour stocker les données
donnees = {
    'Pays': [],
    'Année': [],
    'PIB_milliards_USD': [],
    'PIB_par_habitant_USD': [],
    'Taux_croissance_pct': [],
    'Population_millions': []
}

# Valeurs de base réalistes pour 2015 (en milliards USD)
pib_base = {
    'États-Unis': 18206, 'Chine': 11061, 'Japon': 4444,
    'Allemagne': 3371, 'Inde': 2104, 'Royaume-Uni': 2928,
    'France': 2439, 'Brésil': 1802, 'Canada': 1556,
    'Afrique du Sud': 317
}

# Taux de croissance moyens annuels réalistes (%)
taux_croissance_moyen = {
    'États-Unis': 2.3, 'Chine': 6.5, 'Japon': 0.8,
    'Allemagne': 1.5, 'Inde': 6.8, 'Royaume-Uni': 1.7,
    'France': 1.3, 'Brésil': 1.2, 'Canada': 2.1,
    'Afrique du Sud': 1.0
}

# Population de base en millions (2015)
population_base = {
    'États-Unis': 321, 'Chine': 1376, 'Japon': 127,
    'Allemagne': 81, 'Inde': 1311, 'Royaume-Uni': 65,
    'France': 64, 'Brésil': 205, 'Canada': 36,
    'Afrique du Sud': 55
}

# Génération des données pour chaque pays et chaque année
for pays in pays_liste:
    pib_actuel = pib_base[pays]  # PIB de départ
    pop_actuelle = population_base[pays]  # Population de départ
    
    for i, annee in enumerate(annees):
        # Simulation d'un choc COVID-19 en 2020
        if annee == 2020:
            # Contraction économique importante en 2020
            taux = taux_croissance_moyen[pays] - np.random.uniform(8, 12)
        elif annee == 2021:
            # Rebond partiel en 2021
            taux = taux_croissance_moyen[pays] + np.random.uniform(2, 4)
        else:
            # Croissance normale avec légère variation aléatoire
            taux = taux_croissance_moyen[pays] + np.random.uniform(-1, 1)
        
        # Calcul du nouveau PIB basé sur le taux de croissance
        pib_actuel = pib_actuel * (1 + taux / 100)
        
        # Croissance démographique réaliste
        croissance_pop = 0.5 if pays in ['Inde', 'Afrique du Sud'] else 0.3
        pop_actuelle = pop_actuelle * (1 + croissance_pop / 100)
        
        # Calcul du PIB par habitant
        pib_par_hab = (pib_actuel * 1_000_000_000) / (pop_actuelle * 1_000_000)
        
        # Ajout des données au dictionnaire
        donnees['Pays'].append(pays)
        donnees['Année'].append(annee)
        donnees['PIB_milliards_USD'].append(round(pib_actuel, 2))
        donnees['PIB_par_habitant_USD'].append(round(pib_par_hab, 2))
        donnees['Taux_croissance_pct'].append(round(taux, 2))
        donnees['Population_millions'].append(round(pop_actuelle, 2))

# Création du DataFrame pandas
df = pd.DataFrame(donnees)

# Affichage des premières lignes pour vérification
print("✓ Dataset créé avec succès")
print(f"✓ Dimensions : {df.shape[0]} lignes × {df.shape[1]} colonnes")
print("\n📊 Aperçu des données :\n")
print(df.head(10))
```

**Résultat** : Un DataFrame structuré contenant toutes les données économiques nécessaires à l'analyse est maintenant disponible.

---

### 3.3 Nettoyage et transformation des données

**Explication** : Avant l'analyse, nous vérifions la qualité des données, traitons les valeurs manquantes potentielles et créons des variables dérivées utiles pour l'analyse.

```python
# Vérification des valeurs manquantes
print("🔍 Vérification des valeurs manquantes :\n")
valeurs_manquantes = df.isnull().sum()
print(valeurs_manquantes)

# Vérification des types de données
print("\n📋 Types de données :\n")
print(df.dtypes)

# Vérification des doublons
nb_doublons = df.duplicated().sum()
print(f"\n🔄 Nombre de doublons : {nb_doublons}")

# Création de variables dérivées utiles

# 1. Catégorie de pays (développé vs émergent)
pays_developpes = ['États-Unis', 'Japon', 'Allemagne', 'Royaume-Uni', 'France', 'Canada']
df['Categorie'] = df['Pays'].apply(
    lambda x: 'Développé' if x in pays_developpes else 'Émergent'
)

# 2. Région géographique
regions = {
    'États-Unis': 'Amérique du Nord',
    'Canada': 'Amérique du Nord',
    'Brésil': 'Amérique du Sud',
    'Royaume-Uni': 'Europe',
    'Allemagne': 'Europe',
    'France': 'Europe',
    'Chine': 'Asie',
    'Japon': 'Asie',
    'Inde': 'Asie',
    'Afrique du Sud': 'Afrique'
}
df['Region'] = df['Pays'].map(regions)

# 3. Période (pré-COVID, COVID, post-COVID)
def categoriser_periode(annee):
    if annee < 2020:
        return 'Pré-COVID (2015-2019)'
    elif annee in [2020, 2021]:
        return 'COVID (2020-2021)'
    else:
        return 'Post-COVID (2022-2023)'

df['Periode'] = df['Année'].apply(categoriser_periode)

# Tri des données par pays et année
df = df.sort_values(['Pays', 'Année']).reset_index(drop=True)

print("\n✓ Données nettoyées et transformées")
print(f"✓ Nouvelles variables créées : Categorie, Region, Periode")
print("\n📊 Aperçu des données enrichies :\n")
print(df.head())
```

**Résultat** : Les données sont maintenant propres, structurées et enrichies avec des catégories analytiques pertinentes.

---

### 3.4 Sauvegarde du dataset préparé

**Explication** : Nous sauvegardons le dataset nettoyé pour faciliter le partage et les analyses futures.

```python
# Sauvegarde au format CSV
nom_fichier = 'donnees_pib_analyse.csv'
df.to_csv(nom_fichier, index=False, encoding='utf-8')

print(f"✓ Dataset sauvegardé : {nom_fichier}")
print(f"✓ Taille du fichier : {df.memory_usage(deep=True).sum() / 1024:.2f} KB")
```

**Résultat** : Le dataset est maintenant prêt pour l'analyse statistique et les visualisations.

---

## 4. Analyse Statistique Descriptive

### 4.1 Statistiques globales

**Explication** : Nous calculons les statistiques descriptives de base pour comprendre la distribution et les caractéristiques centrales de nos données économiques.

```python
# Statistiques descriptives complètes
print("📊 STATISTIQUES DESCRIPTIVES COMPLÈTES\n")
print("="*80)

# Statistiques pour les variables numériques principales
stats_desc = df[['PIB_milliards_USD', 'PIB_par_habitant_USD', 
                 'Taux_croissance_pct', 'Population_millions']].describe()
print("\n", stats_desc)

# Statistiques par pays
print("\n\n📍 STATISTIQUES PAR PAYS")
print("="*80)

# Calcul des moyennes par pays
moyennes_pays = df.groupby('Pays').agg({
    'PIB_milliards_USD': 'mean',
    'PIB_par_habitant_USD': 'mean',
    'Taux_croissance_pct': 'mean',
    'Population_millions': 'mean'
}).round(2)

# Tri par PIB moyen décroissant
moyennes_pays = moyennes_pays.sort_values('PIB_milliards_USD', ascending=False)
print("\n", moyennes_pays)

# Écart-types par pays (mesure de volatilité)
print("\n\n📉 VOLATILITÉ (ÉCART-TYPE) PAR PAYS")
print("="*80)

volatilite = df.groupby('Pays').agg({
    'PIB_milliards_USD': 'std',
    'Taux_croissance_pct': 'std'
}).round(2)
volatilite.columns = ['Volatilité_PIB', 'Volatilité_Croissance']
print("\n", volatilite.sort_values('Volatilité_Croissance', ascending=False))
```

**Interprétation** : Ces statistiques révèlent les tendances centrales, la dispersion des données et la stabilité économique de chaque pays.

---

### 4.2 Comparaison entre pays

**Explication** : Nous comparons les performances économiques relatives des différents pays sur plusieurs dimensions clés.

```python
# Comparaison du PIB total moyen (2015-2023)
print("\n\n🏆 CLASSEMENT DES PAYS PAR PIB MOYEN (2015-2023)")
print("="*80)

classement_pib = df.groupby('Pays')['PIB_milliards_USD'].mean().sort_values(ascending=False)
for i, (pays, pib) in enumerate(classement_pib.items(), 1):
    print(f"{i:2d}. {pays:20s} : {pib:>10,.2f} Mds USD")

# Comparaison du PIB par habitant
print("\n\n💰 CLASSEMENT DES PAYS PAR PIB PAR HABITANT MOYEN")
print("="*80)

classement_pib_hab = df.groupby('Pays')['PIB_par_habitant_USD'].mean().sort_values(ascending=False)
for i, (pays, pib_hab) in enumerate(classement_pib_hab.items(), 1):
    print(f"{i:2d}. {pays:20s} : {pib_hab:>10,.2f} USD")

# Comparaison du taux de croissance moyen
print("\n\n📈 CLASSEMENT DES PAYS PAR TAUX DE CROISSANCE MOYEN")
print("="*80)

classement_croissance = df.groupby('Pays')['Taux_croissance_pct'].mean().sort_values(ascending=False)
for i, (pays, croissance) in enumerate(classement_croissance.items(), 1):
    print(f"{i:2d}. {pays:20s} : {croissance:>6.2f} %")

# Analyse par catégorie (Développé vs Émergent)
print("\n\n🌍 COMPARAISON : PAYS DÉVELOPPÉS vs PAYS ÉMERGENTS")
print("="*80)

comp_categorie = df.groupby('Categorie').agg({
    'PIB_milliards_USD': 'mean',
    'PIB_par_habitant_USD': 'mean',
    'Taux_croissance_pct': 'mean'
}).round(2)
comp_categorie.columns = ['PIB moyen (Mds)', 'PIB/hab moyen (USD)', 'Croissance moy. (%)']
print("\n", comp_categorie)
```

**Interprétation** : Cette comparaison met en évidence les disparités économiques entre nations et les différences de dynamiques de croissance.

---

### 4.3 Évolution temporelle du PIB

**Explication** : Nous analysons comment le PIB de chaque pays a évolué au fil des années, en identifiant les tendances et les ruptures.

```python
# Évolution annuelle du PIB pour chaque pays
print("\n\n📅 ÉVOLUTION DU PIB PAR PAYS ET PAR ANNÉE")
print("="*80)

# Création d'un tableau croisé dynamique
evolution_pib = df.pivot_table(
    values='PIB_milliards_USD',
    index='Pays',
    columns='Année',
    aggfunc='mean'
).round(2)

print("\n", evolution_pib)

# Calcul de la variation totale (2015-2023)
print("\n\n📊 VARIATION TOTALE DU PIB (2015 → 2023)")
print("="*80)

variation_totale = df.groupby('Pays').apply(
    lambda x: ((x[x['Année'] == 2023]['PIB_milliards_USD'].values[0] /
                x[x['Année'] == 2015]['PIB_milliards_USD'].values[0]) - 1) * 100
).sort_values(ascending=False)

for pays, var in variation_totale.items():
    print(f"{pays:20s} : {var:>6.2f} %")

# Identification des années de croissance négative
print("\n\n⚠️  ANNÉES DE RÉCESSION (Croissance négative)")
print("="*80)

recessions = df[df['Taux_croissance_pct'] < 0][['Pays', 'Année', 'Taux_croissance_pct']]
recessions = recessions.sort_values('Taux_croissance_pct')
print("\n", recessions)
```

**Interprétation** : L'analyse temporelle révèle les trajectoires de développement et la résilience face aux chocs économiques.

---

### 4.4 Taux de croissance annuels

**Explication** : Nous examinons en détail les taux de croissance pour identifier les périodes de forte expansion ou de contraction.

```python
# Statistiques sur les taux de croissance
print("\n\n📈 ANALYSE DES TAUX DE CROISSANCE")
print("="*80)

# Taux de croissance moyen par période
croissance_periode = df.groupby('Periode')['Taux_croissance_pct'].agg(['mean', 'min', 'max']).round(2)
croissance_periode.columns = ['Moyenne', 'Minimum', 'Maximum']
print("\nTaux de croissance par période :")
print(croissance_periode)

# Taux de croissance moyen par région
croissance_region = df.groupby('Region')['Taux_croissance_pct'].mean().sort_values(ascending=False).round(2)
print("\n\nTaux de croissance moyen par région :")
for region, taux in croissance_region.items():
    print(f"{region:20s} : {taux:>6.2f} %")

# Identification des meilleures et pires performances
print("\n\n🏆 MEILLEURES PERFORMANCES ANNUELLES")
print("="*80)
meilleures = df.nlargest(5, 'Taux_croissance_pct')[['Pays', 'Année', 'Taux_croissance_pct']]
print(meilleures.to_string(index=False))

print("\n\n📉 PIRES PERFORMANCES ANNUELLES")
print("="*80)
pires = df.nsmallest(5, 'Taux_croissance_pct')[['Pays', 'Année', 'Taux_croissance_pct']]
print(pires.to_string(index=False))
```

**Interprétation** : Cette analyse permet d'identifier les moteurs de croissance et les vulnérabilités économiques.

---

### 4.5 Corrélations et tendances

**Explication** : Nous calculons les corrélations entre variables pour identifier les relations économiques significatives.

```python
# Matrice de corrélation
print("\n\n🔗 MATRICE DE CORRÉLATION")
print("="*80)

# Sélection des variables numériques pertinentes
variables_num = ['PIB_milliards_USD', 'PIB_par_habitant_USD', 
                 'Taux_croissance_pct', 'Population_millions']

# Calcul de la matrice de corrélation
matrice_corr = df[variables_num].corr().round(3)
print("\n", matrice_corr)

# Identification des corrélations fortes (|r| > 0.7)
print("\n\n💡 CORRÉLATIONS SIGNIFICATIVES (|r| > 0.7)")
print("="*80)

# Extraction des paires de variables avec forte corrélation
for i in range(len(variables_num)):
    for j in range(i+1, len(variables_num)):
        corr_val = matrice_corr.iloc[i, j]
        if abs(corr_val) > 0.7:
            print(f"{variables_num[i]:30s} ↔ {variables_num[j]:30s} : r = {corr_val:.3f}")

# Corrélation entre PIB et croissance par pays
print("\n\n📊 CORRÉLATION PIB-CROISSANCE PAR PAYS")
print("="*80)

for pays in pays_liste:
    df_pays = df[df['Pays'] == pays]
    corr = df_pays['PIB_milliards_USD'].corr(df_pays['Taux_croissance_pct'])
    print(f"{pays:20s} : r = {corr:>6.3f}")
```

**Interprétation** : Les corrélations identifiées révèlent les interdépendances économiques et les facteurs structurels de développement.

---

## 5. Visualisations Graphiques

### 5.1 Graphique d'évolution du PIB au fil du temps

**Explication** : Ce graphique en ligne montre l'évolution du PIB de chaque pays sur la période 2015-2023, permettant de visualiser les trajectoires de croissance et les impacts des chocs économiques.

```python
# Configuration de la figure
plt.figure(figsize=(16, 10))

# Création du graphique principal
for pays in pays_liste:
    # Filtrage des données pour le pays actuel
    donnees_pays = df[df['Pays'] == pays]
    
    # Tracé de la ligne d'évolution
    plt.plot(donnees_pays['Année'], 
             donnees_pays['PIB_milliards_USD'],
             marker='o',           # Points de données
             linewidth=2.5,        # Épaisseur de la ligne
             markersize=6,         # Taille des points
             label=pays,           # Légende
             alpha=0.8)            # Transparence

# Ajout d'une ligne verticale pour marquer le début de la COVID-19
plt.axvline(x=2020, color='red', linestyle='--', linewidth=2, 
            alpha=0.5, label='Début COVID-19')

# Configuration des titres et labels
plt.title('Évolution du PIB par Pays (2015-2023)\nImpact de la Pandémie COVID-19',
          fontsize=18, fontweight='bold', pad=20)
plt.xlabel('Année', fontsize=14, fontweight='bold')
plt.ylabel('PIB (Milliards USD)', fontsize=14, fontweight='bold')

# Configuration de la grille
plt.grid(True, alpha=0.3, linestyle='-', linewidth=0.5)

# Configuration de la légende
plt.legend(loc='upper left', fontsize=11, framealpha=0.9, ncol=2)

# Configuration des axes
plt.xticks(annees, rotation=45)
plt.tight_layout()

# Affichage du graphique
plt.show()

print("✓ Graphique d'évolution temporelle généré")
```

**Interprétation** : Ce graphique révèle clairement l'impact différencié de la crise COVID-19 selon les économies et les vitesses de reprise variables.

---

### 5.2 Graphique de comparaison du PIB entre pays

**Explication** : Un graphique en barres horizontales comparant le PIB moyen de chaque pays sur la période étudiée, facilitant l'identification des plus grandes économies.

```python
# Calcul du PIB moyen par pays
pib_moyen_pays = df.groupby('Pays')['PIB_milliards_USD'].mean().sort_values()

# Configuration de la figure
plt.figure(figsize=(14, 10))

# Création du graphique en barres horizontales
barres = plt.barh(pib_moyen_pays.index,    # Pays (axe Y)
                   pib_moyen_pays.values,   # PIB (axe X)
                   color='steelblue',       # Couleur des barres
                   alpha
