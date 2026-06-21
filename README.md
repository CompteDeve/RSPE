# 🛒 Système de recommandation d’annonces e-commerce

**Auteur :** Hafssatou Bilal  
**Matricule :** 22067  
**Matière :** MLE413 - Systèmes de recommandation  
**Date :** Juin 2025

---

## 📌 1. Problème

Sur les plateformes e-commerce, les utilisateurs sont souvent submergés par un grand nombre d’annonces. Il devient difficile de trouver rapidement des produits qui correspondent à leurs besoins et préférences.

**Objectif du projet :**  
Créer un système de recommandation qui, à partir d’une annonce consultée par un utilisateur, lui propose **5 annonces similaires** (même catégorie, prix proche, titre ressemblant, localisation proche). Cela permet d’améliorer l’expérience utilisateur et d’augmenter les chances de vente.

---

## 📊 2. Dataset

### Source
Le dataset utilisé est `ecommerce.csv`, un fichier contenant des annonces e-commerce. Il a été fourni dans le cadre du projet.

### Structure
| Colonne | Type | Description |
| :--- | :--- | :--- |
| `ID` | entier | Identifiant unique de l’annonce |
| `Title` | texte | Titre de l’annonce |
| `Category` | texte | Catégorie du produit (ex: Electronics, Clothing, Real Estate) |
| `Price` | texte | Prix avec l’unité "MRU" |
| `Views` | entier | Nombre de vues de l’annonce |
| `Location+Name` | texte | Localisation (ville/quartier) |
| `Link` | texte | Lien vers l’annonce |

### Statistiques
- **Nombre d’annonces :** 6 348
- **Nombre de catégories :** 6
- **Prix moyen :** 260 MRU
- **Vues moyennes :** ~ 45

---

## 🧠 3. Features utilisées

Pour construire le profil de chaque annonce, j’ai utilisé les caractéristiques suivantes :

| Feature | Transformation | Pourquoi |
| :--- | :--- | :--- |
| **Titre** | TF-IDF (500 mots max) | Capturer le contenu textuel et les mots importants |
| **Catégorie** | One-Hot Encoding | Représenter la catégorie sous forme de 0/1 |
| **Prix** | Normalisation MinMax (0-1) | Mettre les prix à la même échelle |
| **Vues** | Normalisation MinMax (0-1) | Prendre en compte la popularité |
| **Localisation** | Nettoyage (suppression des accents/caractères spéciaux) | Uniformiser les noms de lieux |

---

## 🧮 4. Méthode utilisée

### Algorithme
- **Content-Based Filtering** (filtrage basé sur le contenu)
- **Similarité cosinus** pour comparer les profils des annonces

### Étapes principales
1. **Nettoyage** : suppression des valeurs aberrantes, conversion des prix en nombre, nettoyage des localisations.
2. **Feature Engineering** : création d’un vecteur numérique pour chaque annonce (titre, catégorie, prix, vues, localisation).
3. **Calcul de similarité** : chaque annonce est comparée à toutes les autres.
4. **Recommandation** : pour une annonce donnée, on retourne les 5 annonces les plus similaires.

### Outils techniques
- **Python** : langage principal
- **Pandas / NumPy** : manipulation des données
- **Scikit-learn** : TF-IDF, normalisation, similarité cosinus
- **Streamlit** : interface utilisateur interactive
- **Joblib** : sauvegarde des modèles et transformateurs

---

## 📈 5. Évaluation

### Critères d’évaluation
- **Cohérence des recommandations** : les annonces recommandées sont-elles logiquement proches de l’annonce de référence ?
- **Variété des recommandations** : l’algorithme propose-t-il des annonces variées ou toujours les mêmes ?
- **Performance** : temps de réponse de l’application (< 3 secondes).

### Résultats observés
- **90% des recommandations** sont dans la même catégorie.
- Les prix sont généralement proches (différence moyenne < 50 MRU).
- Les titres partagent souvent des mots-clés communs.
- L’application répond en **moins de 2 secondes**.

---

## 🖥️ 6. Instructions d’installation et d’exécution

### Prérequis
- Python 3.8 ou supérieur installé
- Pip (gestionnaire de paquets Python)

### Installation des dépendances
```bash
pip install -r requirements.txt
