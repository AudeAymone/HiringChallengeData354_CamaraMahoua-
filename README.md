# HiringChallengeData354_CamaraMahoua-
Ce repository repond au Hiring Challenge de Data354.
Ce challenge répond à l'objectif de construire un ETL: 
-> Extraire les données horaires depuis l'API de AirQuino
-> Calculer le CO et le PM2.5 moyen par jour de chaque capteur.
-> Stocker les données résultantes dans une base de données (Cassandra ou mongoDB). Nous avons choisi mongoDB.
-> Fournir un dashboard superset pour visualiser les données.
-> Faire un modèle de ml qui fait du forecasting sur les 2 prochaines heures (Optionnel).
Vous repondrez également aux 2 questions suivantes:
_ Quelle serait votre stratégie de mise en production de votre ETL?
_ Quelle serait votre stratégie pour que declencher votre ETL automatiquement chaque heure?

Les points concernant l'extraction des données, le calcul du CO et le PM2.5 moyen par jour et  le stockage des données résultantes sur mongoDB, vous les trouverez dans le fichier DataTreatment.ipynb.

Les données à traiter sont disponibles sur le fichier Data ou via les liens:
url_1 = 'https://airqino-api.magentalab.it/v3/getStationHourlyAvg/283181971'  
url_2 = 'https://airqino-api.magentalab.it/v3/getStationHourlyAvg/283164601'

Au niveau du stockage des données sur mongoDB, assurez vous d'avoir installer mongoDB. Vous pouvez le téléchager via le lien https://www.mongodb.com/try/download/community-kubernetes-operator. Ensuite, assurez vous de le lancer et de recupérer votre lien de serveur localhost, afin de l'insérer dans le code spécifique dans DataTreatment, si celui-ci est différent de celui déjà présent dans le code.

Pour le point du dashboard sur Apache Superset, je vous renvoie vers cette vidéo pour le processus de téléchargement: https://www.youtube.com/watch?v=mAnp_yugoWM&t=101s
