# HiringChallengeData354_CamaraMahoua-
Ce repository repond au Hiring Challenge de Data354.
Ce challenge répond à l'objectif de construire un ETL: 

-> Extraire les données horaires depuis l'API de AirQuino  
-> Calculer le CO et le PM2.5 moyen par jour de chaque capteur.  
-> Stocker les données résultantes dans une base de données (Cassandra ou mongoDB). Nous avons choisi mongoDB.  
-> Fournir un dashboard superset pour visualiser les données.  
-> Faire un modèle de ml qui fait du forecasting sur les 2 prochaines heures (Optionnel).  

## Extraction des données
Pour l'extraction des données de l'Api Airquino, veuillez utiliser ces url:  

```python
url_1 = 'https://airqino-api.magentalab.it/v3/getStationHourlyAvg/283181971' 
url_2 = 'https://airqino-api.magentalab.it/v3/getStationHourlyAvg/283164601'
```  
Les fichiers sont directement accessibles dans le fichier [Data](./Data).  


## Calcul des constantes  
Voir [DataTreatment.ipynb](./DataTreament.ipynb).  

## Stockage des données sur MongoDB
Ici, tout ce trouve également dans le fichier [Data](./Data).   
Par ailleurs, il est important de notifier que la chaine de connection de votre base de données est très importante pour le bon fonctionnement du script et la connexion effective à votre base de données peu importe la base de données choisi.  
Assurez vous d'avoir MongoDB.  
Vous pouvez accédez à la [version en ligne](https://www.mongodb.com/fr-fr/cloud/atlas/) (celle utilisée pour la réalisation de ce projet). Cela vos facilitera la tâche au niveau de la génération de la chaîne de connexion.

## Dashboard Superset

## Modèle de prediction  
Pour le modèle de prédiction, nous avons choisi Tensorflow puisque nous l'avons déjà utilisé auparant pour d'autres projets.  
Toutefois, les modèles de machine learning tels que ARIMA ou Prophet étaient tous aussi valables.  
Voir [DataTreatment.ipynb](./DataTreament.ipynb).  

## Stratégie de mise en production du ETL

## Stratégie de déclenchement du ETL automatiquement chaque heure
