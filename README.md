# Actemium

## Étape 1 — Exploration des données (EDA)
Avant tout, comprendre ce que tu as. Ton CSV contient ~127 colonnes avec des capteurs, pompes, vannes, débits, etc. Il faut :

Charger le CSV, parser les colonnes Date + Time en index datetime
Vérifier les valeurs manquantes, les doublons, les valeurs aberrantes
Tracer la cible 1_LT_001_PV (niveau du réservoir) dans le temps
Visualiser quelques variables clés (débits FIT, statuts pompes/vannes)
Calculer les corrélations avec la cible

-----------------------------------------------------------------------------------------------------------------

## Étape 2 — Préprocessing
Une fois que tu comprends les données :

Créer un index temporel propre (1 ligne = 1 minute)
Sélectionner les features pertinentes (débits, pompes, vannes, setpoints — cf. guide)
Normaliser les features continues (MinMaxScaler ou StandardScaler)
Créer les features laggés (valeurs à t-1, t-2, ..., t-N) pour les modèles ML
Définir ta fenêtre de prédiction : horizon 10 min recommandé (= 10 pas de temps)
Split train/test en respectant l'ordre temporel (pas de shuffle !)

-----------------------------------------------------------------------------------------------------------------

## Étape 3 — Baseline persistence
Indispensable comme point de référence :

Modèle naïf : prédire que le niveau à t+10 = niveau à t
Calculer MAE et RMSE → c'est le score à battre (-20% minimum)

-----------------------------------------------------------------------------------------------------------------

## Étape 4 — Modèles ML (XGBoost / Random Forest)
Plus simple à entraîner :

Construire la matrice features (lags + variables exogènes)
Entraîner XGBoost ou Random Forest
Évaluer MAE/RMSE vs baseline
Faire une feature importance pour identifier les variables les plus utiles

-----------------------------------------------------------------------------------------------------------------

## Étape 5 — Modèles Deep Learning (LSTM / GRU)
Une fois que le pipeline fonctionne :

Reformater les données en séquences 3D (samples, timesteps, features)
Entraîner un LSTM ou GRU
Comparer avec les résultats ML

-----------------------------------------------------------------------------------------------------------------

## Étape 6 — Évaluation & visualisation

Graphique prédiction vs vérité sur la période de test
Tableau comparatif des modèles (MAE, RMSE, Skill score)
Vérifier visuellement que le modèle réagit bien aux activations de pompes/vannes

-----------------------------------------------------------------------------------------------------------------

## Étape 7 — Analyse d'importance (SHAP)

Appliquer SHAP sur le meilleur modèle ML
Identifier quelles variables expliquent le plus les prédictions

-----------------------------------------------------------------------------------------------------------------

## Étape 8 — Rapport + slides

