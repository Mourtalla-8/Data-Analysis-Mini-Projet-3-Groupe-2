<div align="center">

# 🌟 **Rapport Mini Projet 3 - Groupe 2** 🌟

---

</div>


Ce rapport se concentre sur l'analyse des données issues du dataset **"Airline_customer_satisfaction 2"**, qui comporte **129880 entrées** et **22 variables**. Le but de ce mini-projet est de renforcer les compétences en traitement des données, de l'importation à l'analyse, pour appuyer des prises de décisions basées sur des faits.

En examinant plusieurs aspects de l'expérience client dans l'aviation, tels que **la satisfaction des passagers**, **les types de voyages**, **les retards** et **la qualité des services**, nous avons structuré l'analyse en plusieurs étapes :

- **Imports et Lecture des Données**
- **Préparation des Données**
- **Compréhension des Caractéristiques**
- **Relations entre les Caractéristiques**

L'objectif final est de dégager des tendances et des insights exploitables pour **améliorer la satisfaction des clients** et **optimiser les opérations** des compagnies aériennes.

---
> ## Imports et Lecture des Données
---


```python
import pandas as pd
import numpy as np
import missingno as msno

# Importation de la fonction 'display' de la bibliothèque IPython
# Cette fonction permet d'afficher des objets, tels que des DataFrames, de manière formatée dans un Jupyter Notebook,
from IPython.display import display

# Importer le module statsmodels.api pour effectuer des analyses statistiques, y compris la régression linéaire
import statsmodels.api as sm

import matplotlib.pyplot as plt
import seaborn as sns
```

### **Description du Dataset**

#### **1. Aperçu général**
- **Nombre total d'entrées :** 129 880
- **Nombre total de colonnes :** 22

---

#### **2. Détails des Colonnes**

##### 1. `satisfaction`
- **Type :** `object`
- **Description :** Niveau de satisfaction des clients (exemple : `satisfied`, `dissatisfied`).

##### 2. `Type de Client`
- **Type :** `object`
- **Description :** Catégorie du client (exemple : `Loyal Customer`, `Disloyal Customer`).

##### 3. `Âge`
- **Type :** `int64`
- **Description :** Âge des clients en années.

##### 4. `Type de Voyage`
- **Type :** `object`
- **Description :** Type de voyage (exemple : `Personal Travel`, `Business Travel`).

##### 5. `Classe`
- **Type :** `object`
- **Description :** Classe de vol (exemple : `Eco`, `Business`, `Eco Plus`).

##### 6. `Distance de Vol`
- **Type :** `int64`
- **Description :** Distance parcourue en kilomètres.

##### 7. `Confort du Siège`
- **Type :** `int64`
- **Description :** Évaluation du confort du siège (échelle de 0 à 5).

##### 8. `Heure Départ/Arrivée Convenable`
- **Type :** `int64`
- **Description :** Évaluation de la convenance des horaires de départ et d'arrivée.

##### 9. `Nourriture et Boissons`
- **Type :** `int64`
- **Description :** Évaluation de la qualité des repas et boissons.

##### 10. `Emplacement de la Porte`
- **Type :** `int64`
- **Description :** Évaluation de l'emplacement de la porte d'embarquement.

##### 11. `Service Wifi en Vol`
- **Type :** `int64`
- **Description :** Évaluation de la qualité du service Wi-Fi en vol.

##### 12. `Divertissement en Vol`
- **Type :** `int64`
- **Description :** Évaluation de la qualité du divertissement à bord.

##### 13. `Support en Ligne`
- **Type :** `int64`
- **Description :** Évaluation de la qualité du support client en ligne.

##### 14. `Facilité de Réservation en Ligne`
- **Type :** `int64`
- **Description :** Évaluation de la facilité d'utilisation de la plateforme de réservation.

##### 15. `Service à Bord`
- **Type :** `int64`
- **Description :** Évaluation du service à bord.

##### 16. `Service d’Espace pour les Jambes`
- **Type :** `int64`
- **Description :** Évaluation de l'espace pour les jambes.

##### 17. `Gestion des Bagages`
- **Type :** `int64`
- **Description :** Évaluation de la gestion des bagages.

##### 18. `Service d’Enregistrement`
- **Type :** `int64`
- **Description :** Évaluation de la qualité du service d'enregistrement.

##### 19. `Propreté`
- **Type :** `int64`
- **Description :** Évaluation de la propreté de l'avion.

##### 20. `Embarquement en Ligne`
- **Type :** `int64`
- **Description :** Évaluation de l'efficacité de l'embarquement en ligne.

##### 21. `Retard au Départ en Minutes`
- **Type :** `int64`
- **Description :** Retard au départ en minutes.

##### 22. `Retard à l’Arrivée en Minutes`
- **Type :** `float64`
- **Description :** Retard à l'arrivée en minutes.
- **Valeurs manquantes :** 393 valeurs manquantes.

---

#### **3. Analyse des Données**

##### **Types de Données** :
- **1 colonne** de type `float64` (Retard à l’Arrivée en Minutes)
- **17 colonnes** de type `int64` (principalement des évaluations sur différents aspects des vols)
- **4 colonnes** de type `object` (catégories textuelles)

##### **Valeurs manquantes** :
- La colonne `Retard à l’Arrivée en Minutes` contient 393 valeurs manquantes.
- Toutes les autres colonnes ont des valeurs complètes.

---
> ## **Préparation des Données**
---

### **Conversion des Types de Données pour Optimisation Mémoire**

#### Vérification des Valeurs Uniques Avant Conversion
- **Satisfaction** : 2 valeurs uniques
- **Type de Client** : 2 valeurs uniques
- **Type de Voyage** : 2 valeurs uniques
- **Classe** : 3 valeurs uniques

Pour optimiser la mémoire, **nous avons converti** ces colonnes en type **category**. Cette approche permet de **réduire l'espace mémoire** et d'**améliorer les performances** lors de la manipulation des données, assurant ainsi une gestion plus efficace de notre projet.

---


### **Vérifier les doublons**


#### Compter le nombre de valeurs dupliquées dans le dataset




    0


---

### **Vérifier les valeurs manquantes**



#### **Visualiser la matrice des valeurs manquantes**


    
![png](Mini%20Projet%203%20-%20Groupe%202%20_files/Mini%20Projet%203%20-%20Groupe%202%20_24_0.png)
    


#### **Tableau des valeurs manquantes par colonne après suppression**


<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Missing Values</th>
      <th>Percentage</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>satisfaction</th>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>Type de Client</th>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>Âge</th>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>Type de Voyage</th>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>Classe</th>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>Distance de Vol</th>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>Confort du Siège</th>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>Heure Départ/Arrivée Convenable</th>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>Nourriture et Boissons</th>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>Emplacement de la Porte</th>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>Service Wifi en Vol</th>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>Divertissement en Vol</th>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>Support en Ligne</th>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>Facilité de Réservation en Ligne</th>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>Service à Bord</th>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>Service d’Espace pour les Jambes</th>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>Gestion des Bagages</th>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>Service d’Enregistrement</th>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>Propreté</th>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>Embarquement en Ligne</th>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>Retard au Départ en Minutes</th>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>Retard à l’Arrivée en Minutes</th>
      <td>0</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
</div>


---

### **Vérifier les valeurs aberrantes**



#### **Résumé statistique des colonnes numériques**



<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Âge</th>
      <th>Distance de Vol</th>
      <th>Confort du Siège</th>
      <th>Heure Départ/Arrivée Convenable</th>
      <th>Nourriture et Boissons</th>
      <th>Emplacement de la Porte</th>
      <th>Service Wifi en Vol</th>
      <th>Divertissement en Vol</th>
      <th>Support en Ligne</th>
      <th>Facilité de Réservation en Ligne</th>
      <th>Service à Bord</th>
      <th>Service d’Espace pour les Jambes</th>
      <th>Gestion des Bagages</th>
      <th>Service d’Enregistrement</th>
      <th>Propreté</th>
      <th>Embarquement en Ligne</th>
      <th>Retard au Départ en Minutes</th>
      <th>Retard à l’Arrivée en Minutes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>129487.000000</td>
      <td>129487.000000</td>
      <td>129487.000000</td>
      <td>129487.000000</td>
      <td>129487.000000</td>
      <td>129487.000000</td>
      <td>129487.000000</td>
      <td>129487.000000</td>
      <td>129487.000000</td>
      <td>129487.000000</td>
      <td>129487.000000</td>
      <td>129487.000000</td>
      <td>129487.000000</td>
      <td>129487.000000</td>
      <td>129487.000000</td>
      <td>129487.000000</td>
      <td>129487.000000</td>
      <td>129487.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>39.428761</td>
      <td>1981.008974</td>
      <td>2.838586</td>
      <td>2.990277</td>
      <td>2.852024</td>
      <td>2.990377</td>
      <td>3.249160</td>
      <td>3.383745</td>
      <td>3.519967</td>
      <td>3.472171</td>
      <td>3.465143</td>
      <td>3.486118</td>
      <td>3.695460</td>
      <td>3.340729</td>
      <td>3.705886</td>
      <td>3.352545</td>
      <td>14.643385</td>
      <td>15.091129</td>
    </tr>
    <tr>
      <th>std</th>
      <td>15.117597</td>
      <td>1026.884131</td>
      <td>1.392873</td>
      <td>1.527183</td>
      <td>1.443587</td>
      <td>1.305917</td>
      <td>1.318765</td>
      <td>1.345959</td>
      <td>1.306326</td>
      <td>1.305573</td>
      <td>1.270755</td>
      <td>1.292079</td>
      <td>1.156487</td>
      <td>1.260561</td>
      <td>1.151683</td>
      <td>1.298624</td>
      <td>37.932867</td>
      <td>38.465650</td>
    </tr>
    <tr>
      <th>min</th>
      <td>7.000000</td>
      <td>50.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>27.000000</td>
      <td>1359.000000</td>
      <td>2.000000</td>
      <td>2.000000</td>
      <td>2.000000</td>
      <td>2.000000</td>
      <td>2.000000</td>
      <td>2.000000</td>
      <td>3.000000</td>
      <td>2.000000</td>
      <td>3.000000</td>
      <td>2.000000</td>
      <td>3.000000</td>
      <td>3.000000</td>
      <td>3.000000</td>
      <td>2.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>40.000000</td>
      <td>1924.000000</td>
      <td>3.000000</td>
      <td>3.000000</td>
      <td>3.000000</td>
      <td>3.000000</td>
      <td>3.000000</td>
      <td>4.000000</td>
      <td>4.000000</td>
      <td>4.000000</td>
      <td>4.000000</td>
      <td>4.000000</td>
      <td>4.000000</td>
      <td>3.000000</td>
      <td>4.000000</td>
      <td>4.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>51.000000</td>
      <td>2543.000000</td>
      <td>4.000000</td>
      <td>4.000000</td>
      <td>4.000000</td>
      <td>4.000000</td>
      <td>4.000000</td>
      <td>4.000000</td>
      <td>5.000000</td>
      <td>5.000000</td>
      <td>4.000000</td>
      <td>5.000000</td>
      <td>5.000000</td>
      <td>4.000000</td>
      <td>5.000000</td>
      <td>4.000000</td>
      <td>12.000000</td>
      <td>13.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>85.000000</td>
      <td>6951.000000</td>
      <td>5.000000</td>
      <td>5.000000</td>
      <td>5.000000</td>
      <td>5.000000</td>
      <td>5.000000</td>
      <td>5.000000</td>
      <td>5.000000</td>
      <td>5.000000</td>
      <td>5.000000</td>
      <td>5.000000</td>
      <td>5.000000</td>
      <td>5.000000</td>
      <td>5.000000</td>
      <td>5.000000</td>
      <td>1592.000000</td>
      <td>1584.000000</td>
    </tr>
  </tbody>
</table>
</div>




#### **Identification des valeurs aberrantes**

    Variable: Distance de Vol
    Nombre de valeurs aberrantes: 2575
    Pourcentage de valeurs aberrantes: 1.99%
    Valeurs aberrantes: [6792 6591 6470 ... 4652 5403 4522]
    
    
    Variable: Service à Bord
    Nombre de valeurs aberrantes: 13228
    Pourcentage de valeurs aberrantes: 10.22%
    Valeurs aberrantes: [1 1 1 ... 1 1 1]
    
    
    Variable: Service d’Enregistrement
    Nombre de valeurs aberrantes: 15323
    Pourcentage de valeurs aberrantes: 11.83%
    Valeurs aberrantes: [1 1 1 ... 1 1 1]
    
    
    Variable: Retard au Départ en Minutes
    Nombre de valeurs aberrantes: 17970
    Pourcentage de valeurs aberrantes: 13.88%
    Valeurs aberrantes: [310  47  40 ... 155 193 185]
    
    
    Variable: Retard à l’Arrivée en Minutes
    Nombre de valeurs aberrantes: 17492
    Pourcentage de valeurs aberrantes: 13.51%
    Valeurs aberrantes: [305.  48.  48. ... 163. 205. 186.]
    
    
    

Les résultats montrent que certaines variables de notre dataset contiennent des valeurs aberrantes, notamment `Distance de Vol`, `Service à Bord`, `Service d’Enregistrement`, `Retard au Départ en Minutes`, et `Retard à l’Arrivée en Minutes`.
Ces valeurs aberrantes peuvent indiquer des cas extrêmes qui méritent d'être examinés plus en détail pour déterminer s'ils représentent des erreurs de saisie ou des situations réelles.



#### **Boxplots des variables qui contiennent des valeurs aberrantes**


    
![png](Mini%20Projet%203%20-%20Groupe%202%20_files/Mini%20Projet%203%20-%20Groupe%202%20_32_0.png)
    


#### **Interprétation des Résultats**

1. **`Distance de Vol` :** Les valeurs aberrantes observées sont considérées comme normales selon les recherches effectuées. De plus, elles représentent une proportion relativement faible par rapport à l'ensemble des données, ce qui ne pose pas de problème significatif.

2. **`Service d’Enregistrement` :** Les notes aberrantes identifiées sur une échelle de 0 à 5 sont également jugées normales, ne remettant pas en cause la qualité des données.

3. **`Service à Bord` :** Comme pour le service d'enregistrement, les valeurs aberrantes sont des notes dans la même échelle de 0 à 5 et sont considérées comme acceptables.

4. **`Retard au Départ en Minutes` et `Retard à l’Arrivée en Minutes` :** Bien que des retards de plus de 10 heures soient rares, ils peuvent survenir pour des raisons telles que des conditions météorologiques extrêmes, des problèmes techniques ou des grèves. Ces valeurs, bien que élevées, ne représentent pas un nombre significatif par rapport au total des enregistrements.

#### **Conclusion**
L'analyse des valeurs aberrantes a révélé que, bien que certaines valeurs soient considérées comme atypiques, elles restent justifiables et ne compromettent pas l'intégrité des données. Les valeurs de distance de vol, ainsi que les notes des services d'enregistrement et à bord, sont toutes acceptables et n'indiquent pas de problèmes significatifs. De plus, les retards au départ et à l'arrivée, bien que rares, peuvent s'expliquer par des circonstances exceptionnelles. Par conséquent, **ces données peuvent être conservées pour une analyse plus approfondie, sans nécessiter de traitement ou d'exclusion**.


---
> ## **Compréhension des Caractéristiques**
---

Dans cette section, nous analysons les caractéristiques des données afin d'en extraire des informations significatives. Puisque l’objectif est de rester pertinent, nous nous concentrons uniquement sur les variables quantitatives les plus importantes dans notre dataset.

**Variables Quantitatives Sélectionnées**

- **Âge**
- **Distance de Vol**
- **Retard au Départ en Minutes**
- **Retard à l’Arrivée en Minutes**

---

### **Statistiques Descriptives des Variables Quantitatives**

Nous débutons par une analyse **statistique descriptive** des variables quantitatives sélectionnées afin de comprendre leur échelle, leur moyenne et leur dispersion.



<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Âge</th>
      <th>Distance de Vol</th>
      <th>Retard au Départ en Minutes</th>
      <th>Retard à l’Arrivée en Minutes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>129487.000000</td>
      <td>129487.000000</td>
      <td>129487.000000</td>
      <td>129487.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>39.428761</td>
      <td>1981.008974</td>
      <td>14.643385</td>
      <td>15.091129</td>
    </tr>
    <tr>
      <th>std</th>
      <td>15.117597</td>
      <td>1026.884131</td>
      <td>37.932867</td>
      <td>38.465650</td>
    </tr>
    <tr>
      <th>min</th>
      <td>7.000000</td>
      <td>50.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>27.000000</td>
      <td>1359.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>40.000000</td>
      <td>1924.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>51.000000</td>
      <td>2543.000000</td>
      <td>12.000000</td>
      <td>13.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>85.000000</td>
      <td>6951.000000</td>
      <td>1592.000000</td>
      <td>1584.000000</td>
    </tr>
  </tbody>
</table>
</div>



#### **Analyse des Variables Quantitatives**

##### Âge
- **Âge moyen** : 39,4 ans
- **Écart-type** : 15,1  
  Indique une dispersion notable autour de la moyenne, avec une population assez diversifiée.
- **Âge minimal** : 7 ans
- **Âge maximal** : 85 ans  
  Montre la présence de jeunes et de personnes âgées parmi les passagers.
- **Médiane** : 40 ans  
  La moitié des passagers a moins de 40 ans.

##### Distance de Vol
- **Distance moyenne** : 1981 km
- **Écart-type** : 1026 km  
  Montre une forte diversité dans la longueur des trajets.
- **Distance minimale** : 50 km
- **Distance maximale** : 6951 km  
  Illustre la variété des types de vols.
- **Médiane** : 1924 km  
  La majorité des vols sont de distance moyenne.

##### Retard au Départ en Minutes
- **Médiane** : 0 minute  
  La majorité des vols n'ont pas de retard au départ.
- **Retard moyen** : 14,6 minutes
- **Écart-type** : 37,9 minutes  
  Indique des retards considérables pour certains vols.
- **Retard maximal** : 1592 minutes (environ 26,5 heures)  
  Un cas extrême mais possible.

##### Retard à l’Arrivée en Minutes
- **Médiane** : 0 minute  
  Comme pour les départs, la majorité des vols n’ont pas de retard à l’arrivée.
- **Retard moyen** : 15 minutes
- **Écart-type** : 38,4 minutes  
  Montre des écarts similaires à ceux du départ.
- **Retard maximal** : 1584 minutes (environ 26,4 heures)  
  Cas extrêmes, bien que rares.

---

### **Distribution des Variables Catégoriques**

Nous analysons également les variables catégoriques pour comprendre la répartition des passagers en termes de satisfaction, type de client, type de voyage et classe.



    Satisfaction des Clients
    


<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Satisfaction</th>
      <th>Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>satisfied</td>
      <td>70882</td>
    </tr>
    <tr>
      <th>1</th>
      <td>dissatisfied</td>
      <td>58605</td>
    </tr>
  </tbody>
</table>
</div>


    Type de Client
    


<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Type de Client</th>
      <th>Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Loyal Customer</td>
      <td>105773</td>
    </tr>
    <tr>
      <th>1</th>
      <td>disloyal Customer</td>
      <td>23714</td>
    </tr>
  </tbody>
</table>
</div>


    Type de Voyage
    


<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Type de Voyage</th>
      <th>Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Business travel</td>
      <td>89445</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Personal Travel</td>
      <td>40042</td>
    </tr>
  </tbody>
</table>
</div>


    Classe des Passagers
    


<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Classe</th>
      <th>Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Business</td>
      <td>61990</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Eco</td>
      <td>58117</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Eco Plus</td>
      <td>9380</td>
    </tr>
  </tbody>
</table>
</div>


#### **Analyse des Variables Catégoriques**

##### Satisfaction
- **Clients satisfaits** : 70 882 (environ 55%)
- **Clients insatisfaits** : 58 605 (environ 45%)  
  Indique un besoin d'amélioration dans certains aspects du service.

##### Type de Client
- **Clients fidèles** : 105 773 (environ 82%)
- **Clients occasionnels** : 23 714 (environ 18%)  
  Une proportion élevée de clients fidèles pourrait indiquer une bonne fidélisation, mais cela souligne aussi la nécessité d'attirer de nouveaux clients.

##### Type de Voyage
- **Voyages d'affaires** : 89 445 (environ 69%)
- **Voyages personnels** : 40 042 (environ 31%)  
  Une forte demande pour les voyages d'affaires, ce qui pourrait influencer les stratégies de marketing.

##### Classe
- **Classe affaires** : 61 990 (environ 48%)
- **Classe économique** : 58 117 (environ 45%)
- **Classe économique plus** : 9 380 (environ 7%)  
  La répartition des passagers dans les différentes classes peut influencer les décisions concernant l'allocation des ressources.

---

### **Conclusion**

Les résultats montrent une diversité significative dans l’âge des passagers, ainsi que dans les types de vols effectués, avec une répartition variée entre courts et longs courriers. Les retards, bien que peu fréquents en général, peuvent atteindre des durées exceptionnelles dans de rares cas. Du côté des variables catégoriques, une majorité de clients sont satisfaits, fidèles et voyagent pour affaires, souvent en classe affaires ou économique. Cela souligne l'importance d'optimiser les services et de répondre aux attentes des clients pour maintenir leur satisfaction et fidélité.

---
> ## **Relations entre les Caractéristiques**
---

Dans cette section, nous allons explorer les relations entre différentes caractéristiques du dataset afin de dégager des informations clés sur les facteurs influençant la satisfaction des clients, les retards, et d'autres aspects pertinents. Nous adopterons une approche analytique intégrée, combinant corrélations, tests statistiques, régressions et visualisations pour tirer des conclusions significatives.

---

### 1.**Analyse des Corrélations entre Variables Quantitatives**

Nous commencerons par examiner la corrélation entre les variables quantitatives pour déterminer comment elles s'influencent mutuellement. Cela nous aidera à identifier les variables les plus significatives qui peuvent impacter la satisfaction des clients et les retards.


#### **Visualisation de la matrice de corrélation**


    
![png](Mini%20Projet%203%20-%20Groupe%202%20_files/Mini%20Projet%203%20-%20Groupe%202%20_45_0.png)
    


#### **Interprétation**

**Confort du Siège** et **Nourriture et Boissons** (**0.72**) : Corrélation forte ; un bon confort des sièges améliore la satisfaction des passagers concernant la nourriture et les boissons.

**Service Wifi en Vol** et **Embarquement en Ligne** (**0.63**) : Corrélation modérée ; les passagers satisfaits du wifi tendent également à apprécier l'embarquement en ligne, indiquant une préférence pour les services numériques.

**Retard au Départ** et à l’**Arrivée** (**0.97**) : Corrélation presque parfaite ; un retard au départ se traduit généralement par un retard à l'arrivée, soulignant l'impact des départs tardifs.

**En résumé**
Les corrélations montrent que le confort des sièges améliore aussi la satisfaction concernant la nourriture. Les passagers qui apprécient le wifi en vol sont également ceux qui favorisent l'embarquement en ligne. Enfin, un retard au départ est fortement lié à un retard à l’arrivée.

---

### 2. **Test de Chi-2 pour les Variables Catégorielles**

Nous utiliserons le test de Chi-2 pour analyser les relations entre les variables catégorielles, telles que la **satisfaction** et **type de client**, **Satisfaction** et **Classe**, **Satisfaction** et **Type de Voyage**. Ce test nous aidera à déterminer si les distributions observées diffèrent significativement des distributions attendues.

- #### **Satisfaction et Type de Client** :

    **Résultats du test**



    (11081.641807674954, 0.0)



**Valeur du Chi-2** : 11081.64,
**Valeur** p : 0.0

**Interprétation** : La valeur du Chi-2 est très élevée, et la valeur p est extrêmement faible (inférieure à 0.05). Cela indique qu'il existe une forte dépendance entre le Type de Client (Nouveau ou Fidèle) et le niveau de Satisfaction. En d'autres termes, le type de client influence significativement la satisfaction des passagers. Il est probable que les clients fidèles aient tendance à être plus satisfaits que les nouveaux clients, probablement en raison de leur familiarité avec les services ou des avantages liés à leur fidélité.

- #### **Satisfaction et Classe** :

  **Résultats du test**



    (12635.400608233214, 0.0)



**Valeur du Chi-2** : 12635.40,
**Valeur p** : 0.0

**Interprétation** : Le Chi-2 est encore plus élevé pour cette relation, ce qui montre une très forte dépendance entre la Classe (Économique, Affaires, ou Première) et la Satisfaction. Cela signifie que la classe de voyage a un impact significatif sur la satisfaction des passagers. Il est probable que les passagers des classes Affaires et Première soient plus satisfaits que ceux de la classe Économique, en raison de meilleurs services et de plus de confort.

- #### **Satisfaction et Type de Voyage** :

    **Résultats du test**



    (1535.426292974157, 0.0)



**Valeur du Chi-2** : 1535.42, 
**Valeur p** : 0.0

**Interprétation** : Bien que la valeur du Chi-2 soit plus faible que pour les autres variables, elle reste très élevée, ce qui indique une relation significative entre le Type de Voyage (Affaires ou Personnel) et la Satisfaction. Les passagers voyageant pour des raisons professionnelles peuvent avoir des attentes différentes ou des besoins spécifiques, ce qui influence leur satisfaction. Par exemple, les voyageurs d'affaires pourraient être plus exigeants concernant la ponctualité ou la commodité, ce qui peut affecter leur niveau de satisfaction.

---

### 3. **Régression Linéaire pour Analyser les Relations**

Dans cette section, nous allons examiner comment certaines variables quantitatives influencent les retards au départ et à l'arrivée. Cette analyse nous permettra d'identifier les facteurs qui peuvent avoir un impact significatif sur la satisfaction des clients.

---

- #### **Modèle de Régression pour les Retards au Départ**

Nous allons analyser les relations entre les retards au départ et plusieurs variables, telles que la distance de vol, le confort du siège, et la qualité des services.


**Résumé du modèle**



<table class="simpletable">
<caption>OLS Regression Results</caption>
<tr>
  <th>Dep. Variable:</th>    <td>Retard au Départ en Minutes</td> <th>  R-squared:         </th>  <td>   0.014</td>  
</tr>
<tr>
  <th>Model:</th>                        <td>OLS</td>             <th>  Adj. R-squared:    </th>  <td>   0.014</td>  
</tr>
<tr>
  <th>Method:</th>                  <td>Least Squares</td>        <th>  F-statistic:       </th>  <td>   367.7</td>  
</tr>
<tr>
  <th>Date:</th>                  <td>Tue, 01 Oct 2024</td>       <th>  Prob (F-statistic):</th>   <td>  0.00</td>   
</tr>
<tr>
  <th>Time:</th>                      <td>11:38:00</td>           <th>  Log-Likelihood:    </th> <td>-6.5361e+05</td>
</tr>
<tr>
  <th>No. Observations:</th>           <td>129487</td>            <th>  AIC:               </th>  <td>1.307e+06</td> 
</tr>
<tr>
  <th>Df Residuals:</th>               <td>129481</td>            <th>  BIC:               </th>  <td>1.307e+06</td> 
</tr>
<tr>
  <th>Df Model:</th>                   <td>     5</td>            <th>                     </th>      <td> </td>     
</tr>
<tr>
  <th>Covariance Type:</th>           <td>nonrobust</td>          <th>                     </th>      <td> </td>     
</tr>
</table>
<table class="simpletable">
<tr>
              <td></td>                <th>coef</th>     <th>std err</th>      <th>t</th>      <th>P>|t|</th>  <th>[0.025</th>    <th>0.975]</th>  
</tr>
<tr>
  <th>const</th>                    <td>   12.0996</td> <td>    0.473</td> <td>   25.566</td> <td> 0.000</td> <td>   11.172</td> <td>   13.027</td>
</tr>
<tr>
  <th>Distance de Vol</th>          <td>    0.0041</td> <td>    0.000</td> <td>   39.820</td> <td> 0.000</td> <td>    0.004</td> <td>    0.004</td>
</tr>
<tr>
  <th>Confort du Siège</th>         <td>   -0.3817</td> <td>    0.109</td> <td>   -3.508</td> <td> 0.000</td> <td>   -0.595</td> <td>   -0.168</td>
</tr>
<tr>
  <th>Nourriture et Boissons</th>   <td>   -0.0404</td> <td>    0.104</td> <td>   -0.388</td> <td> 0.698</td> <td>   -0.245</td> <td>    0.164</td>
</tr>
<tr>
  <th>Service à Bord</th>           <td>   -0.8635</td> <td>    0.086</td> <td>  -10.054</td> <td> 0.000</td> <td>   -1.032</td> <td>   -0.695</td>
</tr>
<tr>
  <th>Service d’Enregistrement</th> <td>   -0.3959</td> <td>    0.086</td> <td>   -4.614</td> <td> 0.000</td> <td>   -0.564</td> <td>   -0.228</td>
</tr>
</table>
<table class="simpletable">
<tr>
  <th>Omnibus:</th>       <td>163999.755</td> <th>  Durbin-Watson:     </th>   <td>   1.990</td>  
</tr>
<tr>
  <th>Prob(Omnibus):</th>   <td> 0.000</td>   <th>  Jarque-Bera (JB):  </th> <td>56345389.232</td>
</tr>
<tr>
  <th>Skew:</th>            <td> 6.742</td>   <th>  Prob(JB):          </th>   <td>    0.00</td>  
</tr>
<tr>
  <th>Kurtosis:</th>        <td>104.300</td>  <th>  Cond. No.          </th>   <td>1.02e+04</td>  
</tr>
</table><br/><br/>Notes:<br/>[1] Standard Errors assume that the covariance matrix of the errors is correctly specified.<br/>[2] The condition number is large, 1.02e+04. This might indicate that there are<br/>strong multicollinearity or other numerical problems.



##### **Interprétation**

**R-squared (R²) : 0.014** :
Ce coefficient indique que le modèle explique seulement **1.4 %** de la variance des retards au départ, montrant ainsi sa capacité limitée à prédire ces retards.

###### **Variables Explicatives et Coefficients** :

- **Constante (Intercept)** : 12.10  
  Le retard moyen au départ est de **12.1 minutes** lorsque toutes les autres variables sont constantes.

- **Distance de Vol** : 0.0041  
  Chaque kilomètre supplémentaire augmente le retard au départ de **0.0041 minutes**. Cette relation est significative (**t-statistic de 39.82**), indiquant que la distance de vol a un léger impact sur les retards.

- **Confort du Siège** : -0.3817  
  Une meilleure note pour le confort du siège réduit le retard de **0.38 minutes**, une relation significative suggérant une gestion plus efficace des vols mieux notés.

- **Nourriture et Boissons** : -0.0404  
  Cette variable n'est pas significative (**P > 0.05**), indiquant qu'elle n'influence pas les retards au départ.

- **Service à Bord** : -0.8635  
  Un meilleur service à bord réduit les retards de **0.86 minutes**, avec une signification statistique, ce qui suggère une meilleure gestion des vols.

- **Service d’Enregistrement** : -0.3959  
  Un service d'enregistrement plus efficace est associé à une réduction du retard de **0.40 minutes**, indiquant son influence positive sur la ponctualité des départs.

En résumé, bien que le modèle n'explique qu'une petite portion des retards au départ, certaines variables comme le confort du siège, le service à bord et le service d'enregistrement montrent des impacts significatifs sur la ponctualité. Ces résultats soulignent l'importance d'améliorer ces aspects pour optimiser la gestion des vols et réduire les retards.

___

- #### **Modèle de Régression pour les Retards à l'Arrivée**

Nous allons maintenant examiner les retards à l'arrivée en utilisant les mêmes variables.


**Résumé du modèle**



<table class="simpletable">
<caption>OLS Regression Results</caption>
<tr>
  <th>Dep. Variable:</th>    <td>Retard à l’Arrivée en Minutes</td> <th>  R-squared:         </th>  <td>   0.014</td>  
</tr>
<tr>
  <th>Model:</th>                         <td>OLS</td>              <th>  Adj. R-squared:    </th>  <td>   0.014</td>  
</tr>
<tr>
  <th>Method:</th>                   <td>Least Squares</td>         <th>  F-statistic:       </th>  <td>   369.1</td>  
</tr>
<tr>
  <th>Date:</th>                   <td>Tue, 01 Oct 2024</td>        <th>  Prob (F-statistic):</th>   <td>  0.00</td>   
</tr>
<tr>
  <th>Time:</th>                       <td>11:38:01</td>            <th>  Log-Likelihood:    </th> <td>-6.5541e+05</td>
</tr>
<tr>
  <th>No. Observations:</th>            <td>129487</td>             <th>  AIC:               </th>  <td>1.311e+06</td> 
</tr>
<tr>
  <th>Df Residuals:</th>                <td>129481</td>             <th>  BIC:               </th>  <td>1.311e+06</td> 
</tr>
<tr>
  <th>Df Model:</th>                    <td>     5</td>             <th>                     </th>      <td> </td>     
</tr>
<tr>
  <th>Covariance Type:</th>            <td>nonrobust</td>           <th>                     </th>      <td> </td>     
</tr>
</table>
<table class="simpletable">
<tr>
              <td></td>                <th>coef</th>     <th>std err</th>      <th>t</th>      <th>P>|t|</th>  <th>[0.025</th>    <th>0.975]</th>  
</tr>
<tr>
  <th>const</th>                    <td>   13.3243</td> <td>    0.480</td> <td>   27.764</td> <td> 0.000</td> <td>   12.384</td> <td>   14.265</td>
</tr>
<tr>
  <th>Distance de Vol</th>          <td>    0.0041</td> <td>    0.000</td> <td>   39.230</td> <td> 0.000</td> <td>    0.004</td> <td>    0.004</td>
</tr>
<tr>
  <th>Confort du Siège</th>         <td>   -0.4023</td> <td>    0.110</td> <td>   -3.647</td> <td> 0.000</td> <td>   -0.619</td> <td>   -0.186</td>
</tr>
<tr>
  <th>Nourriture et Boissons</th>   <td>   -0.0667</td> <td>    0.106</td> <td>   -0.631</td> <td> 0.528</td> <td>   -0.274</td> <td>    0.140</td>
</tr>
<tr>
  <th>Service à Bord</th>           <td>   -0.9749</td> <td>    0.087</td> <td>  -11.195</td> <td> 0.000</td> <td>   -1.146</td> <td>   -0.804</td>
</tr>
<tr>
  <th>Service d’Enregistrement</th> <td>   -0.4705</td> <td>    0.087</td> <td>   -5.408</td> <td> 0.000</td> <td>   -0.641</td> <td>   -0.300</td>
</tr>
</table>
<table class="simpletable">
<tr>
  <th>Omnibus:</th>       <td>161119.372</td> <th>  Durbin-Watson:     </th>   <td>   1.987</td>  
</tr>
<tr>
  <th>Prob(Omnibus):</th>   <td> 0.000</td>   <th>  Jarque-Bera (JB):  </th> <td>49165297.366</td>
</tr>
<tr>
  <th>Skew:</th>            <td> 6.561</td>   <th>  Prob(JB):          </th>   <td>    0.00</td>  
</tr>
<tr>
  <th>Kurtosis:</th>        <td>97.554</td>   <th>  Cond. No.          </th>   <td>1.02e+04</td>  
</tr>
</table><br/><br/>Notes:<br/>[1] Standard Errors assume that the covariance matrix of the errors is correctly specified.<br/>[2] The condition number is large, 1.02e+04. This might indicate that there are<br/>strong multicollinearity or other numerical problems.



##### **Interprétation**

- **R-squared (R²) : 0.014**  
  Ce modèle explique seulement **1.4 %** de la variance des retards à l’arrivée, indiquant que d'autres facteurs non inclus influencent également les retards.

###### **Variables Explicatives et Coefficients** :

- **Constante (Intercept) : 13.32**  
  En l'absence des autres variables, le retard moyen à l’arrivée serait de **13.32 minutes**.

- **Distance de Vol : 0.0041**  
  La distance de vol augmente le retard à l’arrivée de **0.0041 minutes par kilomètre**, montrant que des vols plus longs peuvent entraîner des retards plus importants.

- **Confort du Siège : -0.4023**  
  Un meilleur confort du siège réduit les retards à l’arrivée de **0.40 minutes**, suggérant qu'une satisfaction accrue des passagers peut être liée à une meilleure gestion des vols.

- **Nourriture et Boissons : -0.0667**  
  Cette variable n'a pas d'impact significatif sur les retards à l’arrivée (**P > 0.05**).

- **Service à Bord : -0.9749**  
  Un meilleur service à bord réduit le retard à l’arrivée de **0.97 minutes**, soulignant que des services efficaces en vol peuvent réduire les retards.

- **Service d’Enregistrement : -0.4705**  
  Un service d'enregistrement plus efficace réduit les retards à l’arrivée de **0.47 minutes**, indiquant son impact positif sur la ponctualité des vols.

En résumé, bien que le modèle n'explique qu'une faible portion des retards à l’arrivée, des variables telles que le confort du siège, le service à bord et le service d'enregistrement montrent des effets significatifs. Ces résultats soulignent l'importance d'améliorer ces aspects pour réduire les retards à l’arrivée et optimiser la gestion des vols.

---


#### Conclusion sur les deux Modèles de Retard

Les analyses des retards au départ et à l’arrivée révèlent des informations cruciales sur l'impact de diverses variables. Dans les deux modèles, le R-squared (R²) indique que seulement **1.4 %** de la variance des retards est expliquée par les variables sélectionnées, suggérant que d'autres facteurs non inclus dans les modèles jouent un rôle significatif.

Les variables telles que **la distance de vol**, **le confort du siège**, **le service à bord** et **le service d'enregistrement** montrent des relations significatives avec les retards, soulignant l'importance d'améliorer ces aspects pour optimiser la ponctualité. En conclusion, bien que le modèle ait des limitations, il offre des pistes pour des améliorations pratiques dans la gestion des vols et la satisfaction des passagers.

---

### 4. **Analyse des Retards et de la Satisfaction**

Dans cette section, nous analyserons l'impact des retards au départ et à l'arrivée sur la satisfaction des clients. Nous utiliserons à la fois des histogrammes et des graphiques linéaires pour visualiser les relations entre ces variables.

___

- #### **Histogrammes de la Satisfaction en Fonction des Retards**

Nous commencerons par examiner la distribution des retards au départ et à l'arrivée en fonction des niveaux de satisfaction des clients.


    
![png](Mini%20Projet%203%20-%20Groupe%202%20_files/Mini%20Projet%203%20-%20Groupe%202%20_67_0.png)
    



    
![png](Mini%20Projet%203%20-%20Groupe%202%20_files/Mini%20Projet%203%20-%20Groupe%202%20_67_1.png)
    

___

- #### **Évolution des Retards en Fonction de la Satisfaction**

Pour approfondir notre compréhension de l'impact des retards sur la satisfaction, nous allons analyser les moyennes des retards au départ et à l'arrivée pour chaque niveau de satisfaction.


**Moyenne des retards au départ et à l'arrivée pour chaque niveau de satisfaction**



<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>satisfaction</th>
      <th>Retard au Départ en Minutes</th>
      <th>Retard à l’Arrivée en Minutes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>dissatisfied</td>
      <td>17.728777</td>
      <td>18.504599</td>
    </tr>
    <tr>
      <th>1</th>
      <td>satisfied</td>
      <td>12.092393</td>
      <td>12.268883</td>
    </tr>
  </tbody>
</table>
</div>


    
![png](Mini%20Projet%203%20-%20Groupe%202%20_files/Mini%20Projet%203%20-%20Groupe%202%20_69_1.png)



#### **Interprétation des Retards et de la Satisfaction**

L'analyse des histogrammes et de l'évolution des retards en fonction des niveaux de satisfaction met en lumière des tendances significatives :

- **Impact des Retards sur la Satisfaction** :  
  Les histogrammes indiquent que les clients insatisfaits rencontrent des retards plus importants. En moyenne, les retards au départ pour les clients insatisfaits s'élèvent à **17,73 minutes**, tandis que les retards à l'arrivée atteignent **18,50 minutes**. En revanche, les clients satisfaits bénéficient de retards moindres, avec une moyenne de **12,09 minutes** au départ et **12,27 minutes** à l'arrivée.

- **Corrélation entre Retards et Satisfaction** :  
  Cette analyse suggère qu'une diminution des retards pourrait avoir un effet positif sur la satisfaction des clients. L'évolution des retards selon les niveaux de satisfaction renforce cette conclusion, soulignant l'importance d'optimiser les opérations pour réduire les retards.

En résumé, l'amélioration de la ponctualité pourrait non seulement diminuer les retards, mais également contribuer à une expérience client plus positive.

---

### 5. **Analyse des Services par Rapport à la Satisfaction**

Dans cette section, nous allons analyser les moyennes des évaluations de certains services par rapport à la satisfaction des clients. Cela nous permettra d'identifier les services qui pourraient contribuer à l'insatisfaction et d'orienter nos efforts d'amélioration.


#### Visualisation


    
![png](Mini%20Projet%203%20-%20Groupe%202%20_files/Mini%20Projet%203%20-%20Groupe%202%20_73_1.png)
    


#### **Interprétation**

Le graphique illustre les évaluations des différents services en fonction des niveaux de satisfaction des clients. Il est **évident** que :

- **Les clients satisfaits** attribuent des notes nettement plus élevées dans presque tous les domaines.
- Par exemple, **le confort des sièges** et **le service Wi-Fi en vol** montrent un écart significatif entre les deux groupes, soulignant l'impact direct de ces services sur la satisfaction globale.

Cette analyse suggère qu'en ciblant l'amélioration des services perçus comme déficients, l'entreprise peut considérablement **rehausser l'expérience des passagers** et, par conséquent, **augmenter la satisfaction client**.


```python

```

---

<div align="center">

---

# **Conclusion**

---

</div>

Cette analyse des données de satisfaction client offre des insights cruciaux pour améliorer l'expérience des passagers :

- **Impact des Retards :**  
  Les retards au départ et à l'arrivée sont fortement corrélés à la satisfaction. Les clients insatisfaits subissent des retards moyens de **17,73 minutes**, contre **12,09 minutes** pour les satisfaits. Optimiser la ponctualité pourrait donc augmenter significativement la satisfaction client.

- **Influence du Type de Client et de la Classe :**  
  Les clients fidèles, surtout ceux en classe Affaires, affichent une satisfaction supérieure. Maintenir des standards élevés pour ces segments est essentiel pour renforcer leur fidélité.

- **Importance des Services à Bord :**  
  La qualité des services, tels que le confort des sièges, le Wi-Fi, la nourriture, les boissons, et le divertissement, impacte directement la satisfaction. Investir dans ces domaines peut nettement améliorer l'expérience des passagers.

- **Nécessité d'Optimiser les Opérations :**  
  Bien que le modèle n'explique que **1,4 %** de la variance des retards, des facteurs tels que la distance de vol et le service à bord montrent une relation significative, suggérant que d'autres éléments doivent également être pris en compte.

En somme, cette étude souligne l'importance d'une approche centrée sur le client pour améliorer les performances et la satisfaction. En ciblant ces domaines critiques, des décisions stratégiques peuvent être prises pour renforcer la position sur le marché et fidéliser les clients.


```python

```
