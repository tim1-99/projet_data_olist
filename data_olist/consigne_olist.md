# Olist : première analyse des ventes avec pandas

**Journée du lundi 2 novembre 2026 · travail individuel · rendu à 17 h**

---

## Page 1 — Ce que tu vas faire

Mariana, responsable commerciale de la place de marché brésilienne **Olist**, prépare son comité de direction. Elle veut savoir :

1. comment évoluent les ventes dans le temps ;
2. quelles catégories de produits et quelles régions rapportent le plus ;
3. si les retards de livraison font baisser la satisfaction des clients.

Tu vas lui répondre avec pandas, à partir de 6 tables réelles (environ 100 000 commandes, 2016-2018), en suivant **6 missions** dans un seul notebook.

### Compétences visées

**Référentiel WCS** (semaine pandas P6, niveau **2 · Adapter**) :

- **C2.5** Tableaux de données : DataFrames avec Python et pandas — niveau 2
- **C1.1** Identifier les usages possibles des données et en évaluer la qualité — niveau 2
- **C4.2** Visualisations descriptives : nuages, boîtes à moustache, histogrammes — niveau 2

**Référentiel Simplon** (niveau 6) :

- **C8** Développer des règles de nettoyage de données — travaillée partiellement (manquants, doublons, uniformisation des dates)
- **C16** Définir les représentations graphiques adaptées aux objectifs d'analyse

**Niveau 2 · Adapter**, concrètement : chaque mission te donne la méthode, un exemple sur d'autres données et du code à trous. Ton travail est d'adapter tout cela aux données Olist et d'expliquer ce que tu trouves.

---

## Page 2 — Préparer ton poste (15 min, avant 9 h 15)

1. **Crée un dossier** `olist` sur ton poste.
2. **Télécharge le notebook** `3_adapter_pandas_olist.ipynb` (ressource de ce brief) et place-le dans `olist`.
3. **Télécharge les données** : archive déposée dans les ressources de ce brief. À défaut : [Brazilian E-Commerce Public Dataset by Olist (Kaggle)](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce), compte Kaggle gratuit nécessaire.
4. **Dézippe l'archive** dans un sous-dossier nommé exactement `data_olist`. L'archive contient 9 CSV : tu n'en utilises que 6, laisse les autres.
5. **Ouvre le notebook** dans Jupyter ou VS Code et exécute la cellule **0. Chargement des données**. Tu dois voir 6 lignes, de `commandes (99441, 8)` à `traduction (71, 2)`.

Ton dossier doit ressembler à ceci :

```
olist/
├── 3_adapter_pandas_olist.ipynb
└── data_olist/
    ├── olist_orders_dataset.csv
    ├── olist_order_items_dataset.csv
    ├── olist_customers_dataset.csv
    ├── olist_products_dataset.csv
    ├── olist_order_reviews_dataset.csv
    └── product_category_name_translation.csv
```

**Si la cellule 0 plante**

- `FileNotFoundError` : le dossier ne s'appelle pas exactement `data_olist`, ou il n'est pas à côté du notebook.
- `KeyError: 'product_category_name'` : le fichier de traduction a été ouvert et enregistré avec Excel. Retélécharge-le et ne l'ouvre plus avec Excel.

---

## Page 3 — Plan d'action, étape par étape

Tout se passe dans **un seul fichier** : `3_adapter_pandas_olist.ipynb`. Remplis les cellules **dans l'ordre**, de haut en bas. Chaque mission utilise le résultat de la précédente.

Dans chaque mission, tu trouves toujours les mêmes blocs :

- **Méthode** : les étapes à suivre ;
- **📘 Exemple** : la technique montrée sur d'autres données ;
- **cellules de code** : remplace chaque `...` par ton code ;
- **✅ Je vérifie** : des repères chiffrés pour savoir si tu es sur la bonne voie ;
- **Commentaire** : des phrases à compléter, pour Mariana.

### Étape 1 — Mission 1 : Auditer les tables (9 h 20 → 10 h 30)

- **Cellules** : 1.1 à 1.5, puis le commentaire de la mission 1.
- **À faire** : construire le tableau d'audit avec une boucle, compter les statuts, expliquer les dates vides, convertir les dates, vérifier les clés.
- **Tu as fini quand** : le tableau d'audit a 6 lignes et `commandes.dtypes` affiche `datetime64` pour les 5 colonnes de dates.

### Étape 2 — Mission 2 : Construire la table `ventes` (10 h 45 → 12 h 15)

- **Cellules** : 2.1 à 2.4, puis le commentaire de la mission 2.
- **À faire** : filtrer les commandes livrées, joindre les tables une par une dans l'ordre imposé, créer `categorie` et `montant`.
- **Tu as fini quand** : `ventes` a **110 197** lignes et les 4 contrôles de la cellule 2.4 affichent `True`.
- **Priorité** : les missions 1 et 2 sont les plus importantes. Termine-les avant de passer à la suite, même si tu prends du retard.

### Étape 3 — Mission 3 : Évolution des ventes (13 h 30 → 14 h 20)

- **Cellules** : 3.1 à 3.5, puis le commentaire de la mission 3.
- **À faire** : indicateurs par mois, mois incomplets écartés, courbe du CA, mois record.
- **Tu as fini quand** : ta courbe a un titre, des axes nommés, et ton panier moyen est entre 145 et 170 R$.

### Étape 4 — Mission 4 : Catégories et régions (14 h 20 → 15 h 10)

- **Cellules** : 4.1 à 4.4, puis le commentaire de la mission 4.
- **À faire** : parts des catégories, top 10 en barres, CA et commandes par État.
- **Tu as fini quand** : la somme des parts affiche 100 %.

### Étape 5 — Mission 5 : Livraison et satisfaction (15 h 20 → 16 h 20)

- **Cellules** : 5.1 à 5.4, puis le commentaire de la mission 5.
- **À faire** : délai, indicateur de retard, histogramme, une note par commande (règle A ou B), note moyenne selon le retard.
- **Tu as fini quand** : tu trouves **96 470** commandes avec une date de réception et `is_unique` affiche `True`.

### Étape 6 — Mission 6 : Livrer (16 h 20 → 17 h 00)

- **Cellules** : 6.1 (obligatoire), 6.2 (optionnelle), puis la synthèse pour Mariana.
- **À faire** : exporter `ventes_olist.csv`, le relire, rédiger la synthèse en complétant les 5 amorces.
- **Tu as fini quand** : le fichier `ventes_olist.csv` est dans ton dossier `olist` et la synthèse ne contient plus de « … ».

### Si tu as fini en avance

Fais la partie **🚀 Pour aller plus loin** à la fin du notebook, dans l'ordre que tu veux.

---

## Page 4 — Auto-évaluation avant de rendre

Coche chaque case. Une case non cochée = une chose à reprendre avant le dépôt.

**Fiabilité**

- [ ] *Noyau › Redémarrer et tout exécuter* : aucune cellule en erreur.
- [ ] Aucun chiffre n'est tapé à la main dans le code : tout est calculé.
- [ ] `ventes` a 110 197 lignes, et je le prouve dans la cellule 2.4.

**Calculs**

- [ ] Le panier moyen est calculé par commande (`nunique`), pas par article.
- [ ] Les parts des catégories font 100 %.
- [ ] Une commande ne compte qu'une fois dans le calcul des notes.

**Graphiques**

- [ ] Chaque graphique a un titre et des axes nommés, avec l'unité.
- [ ] Pour chaque graphique, j'ai écrit son objectif (évolution, comparaison, distribution).

**Communication**

- [ ] Les 6 commentaires sont remplis, chiffres à l'appui.
- [ ] La synthèse fait 5 à 8 lignes, sans jargon technique, et chaque phrase s'appuie sur un chiffre du notebook.

---

## Page 5 — Rendu et ressources

### À déposer sur Simplonline avant 17 h

1. Le notebook `3_adapter_pandas_olist.ipynb`, **exécuté** (les résultats doivent être visibles).
2. Le fichier `ventes_olist.csv`.

Ne dépose pas le dossier `data_olist` : il est trop lourd et ton formateur l'a déjà.

### Ressources

- Tes notebooks précédents : Iris (niveau 1) et Titanic (niveau 2). Les techniques de sélection, de filtre et de `groupby` y sont déjà montrées.
- Documentation pandas :
  - [Joindre des tables avec `merge`](https://pandas.pydata.org/docs/reference/api/pandas.merge.html)
  - [Convertir des dates avec `to_datetime`](https://pandas.pydata.org/docs/reference/api/pandas.to_datetime.html)
  - [Grouper et agréger avec `groupby`](https://pandas.pydata.org/docs/user_guide/groupby.html)
- Ton cours SQL de la semaine 42 : les jointures `INNER` / `LEFT` fonctionnent de la même façon en pandas.

### Et demain ?

La fin du notebook contient un encart **🌉 Pont vers Power Query**. Garde-le sous la main : mardi, tu referas les mêmes opérations (convertir les types, fusionner des tables, regrouper par mois) dans Power Query.

---

*Données : Olist, « Brazilian E-Commerce Public Dataset », publiées sur Kaggle sous licence CC BY-NC-SA 4.0.*
