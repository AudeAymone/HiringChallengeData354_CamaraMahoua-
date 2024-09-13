# HiringChallengeData354_CamaraMahoua-
Ce repository repond au Hiring Challenge de Data354.
Ce challenge répond à l'objectif de construire un ETL: 

#### -> Extraire les données horaires depuis l'API de AirQuino  
#### -> Calculer le CO et le PM2.5 moyen par jour de chaque capteur.  
#### -> Stocker les données résultantes dans une base de données (Cassandra ou mongoDB). Nous avons choisi mongoDB.  
#### -> Fournir un dashboard superset pour visualiser les données.  
#### -> Faire un modèle de ml qui fait du forecasting sur les 2 prochaines heures (Optionnel).  

## Extraction des données
Pour l'extraction des données de l'Api Airquino, veuillez utiliser ces url:  

```python
url_1 = 'https://airqino-api.magentalab.it/v3/getStationHourlyAvg/283181971' 
url_2 = 'https://airqino-api.magentalab.it/v3/getStationHourlyAvg/283164601'
```  
Les fichiers sont directement accessibles dans le fichier [Data](./Data).  


## Calcul des constantes  
Voir [DataTreatment.ipynb](https://github.com/AudeAymone/HiringChallengeData354_CamaraMahoua-/blob/main/DataTreatment.ipynb).  

## Stockage des données sur MongoDB
Vous trouverez le script correspondant dans le fichier [DataTreatment.ipynb](https://github.com/AudeAymone/HiringChallengeData354_CamaraMahoua-/blob/main/DataTreatment.ipynb).     
Par ailleurs, il est important de notifier que la chaîne de connection de votre base de données est très importante pour le bon fonctionnement du script et la connexion effective à votre base de données peu importe la base de données choisie.  
Assurez vous d'avoir MongoDB.  
Vous pouvez accédez à la [version en ligne de MongoDB](https://www.mongodb.com/fr-fr/cloud/atlas/) (celle utilisée pour la réalisation de ce projet). Cela vos facilitera la tâche au niveau de la génération de la chaîne de connexion.

## Dashboard Superset

Apache Superset est un outil de visualisation de données open-source qui permet de créer des tableaux de bord interactifs et des graphiques à partir de diverses sources de données.  
Il requiert d'être installé en localhost afin de l'utiliser.  
Nous vous avons fourni [ce lien](https://superset.apache.org/docs/quickstart/) afin de l'installer par vous même.  
Aussi, il est important de notifier que superset n'interagit pas nativement avec des données non relationnelles. Pour ce faire, nous avons installé apache drill qui représente une passerelle entre Apache Superset et MongoDb. Cliquez sur [ce lien](https://thedataist.com/visualize-anything-with-superset-and-drill/) afin d'avoir toute la docummentation requise pour l'installation.

Par la suite, il vous faudra connecter votre base de données mongo à Superset. Nous vous avons fourni [ce lien](https://www.youtube.com/watch?v=5wGcPiZCKgc&t=63s) qui résume toutes les étapes de pour la connexion. 

## Modèle de prediction  
Pour le modèle de prédiction, nous avons choisi Tensorflow puisque nous l'avons déjà utilisé auparant pour d'autres projets.  
Toutefois, les modèles de machine learning tels que ARIMA ou Prophet étaient tous aussi valables.  
Voir [DataTreatment.ipynb](https://github.com/AudeAymone/HiringChallengeData354_CamaraMahoua-/blob/main/DataTreatment.ipynb).    

## Stratégie de mise en production du ETL  

### 1.Structuration et Organisation du Code :
_ Segmentez chaque étape de l'ETL (Extraction, Transformation, Chargement) en modules distincts et réutilisables.  
_ Créez des scripts bien documentés pour chaque étape (par exemple, extraction API, transformation des données, prévision des données, etc.).  
_ Utilisez un fichier de configuration externe pour gérer les paramètres de l'API, les informations de la base de données, et les paramètres du modèle, facilitant ainsi les modifications sans toucher au code.  

### 2.Gestion des Environnements :  
_ DevOps : Créez des environnements séparés pour le développement, les tests et la production.
_ Utilisez des conteneurs Docker pour encapsuler le projet avec ses dépendances et faciliter le déploiement sur différents environnements sans conflits de versions.
_ Préparez des scripts pour automatiser le provisionnement des environnements avec Docker Compose ou Kubernetes pour des solutions plus avancées.  

### 3.Orchestration et Planification :  
_ Utilisez un outil d'orchestration comme **Apache Airflow** ou **Luigi** pour planifier et automatiser le déclenchement des tâches ETL.  
_ Configurez des workflows avec des tâches dépendantes (extraction, transformation, chargement, et prévision), permettant ainsi une gestion fine des erreurs et des relances automatiques en cas d'échec.  
_ Mettez en place des plannings d'exécution réguliers, par exemple, l'extraction toutes les heures et les agrégations quotidiennes.


### 4.Gestion des Données et Bases de Données :
_ Si vous utilisez MongoDB ou Cassandra comme bases de données pour les données transformées, configurez une stratégie de réplication pour garantir une haute disponibilité des données en production.  
_ Assurez-vous que les index des bases de données sont optimisés pour les requêtes et les insertions fréquentes.  
_ Surveillez l'usage de l'espace disque et des performances avec des outils de monitoring pour les bases de données NoSQL.  

### 5.Monitoring et Logs :  
_ Implémentez un système de logging centralisé (par exemple avec ELK stack : Elasticsearch, Logstash, Kibana ou Graylog) pour surveiller l'exécution de l'ETL en temps réel.  
_ Activez des alertes automatisées (par exemple avec Prometheus et Grafana) en cas d’échec ou d’erreur critique dans le processus ETL.  
_ Capturez les métriques clés (temps d'exécution des jobs, taux d’erreur, etc.) pour améliorer la maintenance et le dépannage.  

### 6.Gestion des Modèles de Prédiction :  
_ Entraînez régulièrement les modèles (comme LSTM ou ARIMA) sur les données nouvelles pour maintenir les performances prédictives à jour.  
_ Intégrez le versioning des modèles (par exemple avec MLflow ou DVC) pour suivre les performances et éviter de déployer un modèle dégradé.  
_ Automatiser la mise à jour des modèles et le passage en production à l’aide de pipelines CI/CD, où le modèle est validé et déployé.  

### 7.Sécurisation et Authentification :  
_ Pour la connexion à des bases de données comme MongoDB Atlas, utilisez des connexions sécurisées SSL et des clés API pour protéger les échanges de données.  
_ Mettez en place un système de gestion des utilisateurs avec des permissions pour restreindre les accès à certaines ressources critiques (par exemple, restreindre les accès en écriture aux bases de données en production).  

### 8.Intégration avec Superset :  
_ Préparez un connecteur pour intégrer les données agrégées et transformées dans Superset.  
_ Configurez des tableaux de bord interactifs pour visualiser les données et les prévisions en temps réel.  
_ Automatisez les actualisations des tableaux de bord pour qu’ils soient toujours à jour avec les dernières données.  

### 9.Tests et Validation :  
_ Établissez des tests unitaires et d'intégration pour chaque étape du pipeline ETL pour garantir sa stabilité.  
_ Effectuez des tests de charge sur les étapes de transformation et de chargement pour vous assurer que le système peut gérer des volumes élevés de données en production.  
_ Validez régulièrement la qualité des prévisions générées par le modèle en les comparant avec des données réelles non observées lors de l’entraînement.  

### 10.Documentation et Maintenance:  
_ Fournissez une documentation complète décrivant le flux ETL, les dépendances, et les procédures de déploiement.  
_ Créez un plan de maintenance régulier, avec des revues de performance et des ajustements pour garantir la scalabilité et la disponibilité du système.  


## Stratégie de déclenchement du ETL automatiquement chaque heure  

### Utilisation d’un Planificateur de Tâches :  
**Cron (Linux)** : Utilisez cron pour planifier l'exécution automatique du script ETL toutes les heures. Vous pouvez configurer un job cron pour appeler le script Python qui exécute l’ETL.  
_Commande pour éditer le cron job:  
```bash
crontab -e
```

_Ajouter la ligne suivante pour exécuter le script ETL chaque heure:  
```bash
0 * * * * /usr/bin/python3 /path/to/your_etl_script.py >> /path/to/logfile.log 2>&1
```

_Assurez-vous de capturer les logs pour surveiller les échecs et les succès.

**Task Scheduler (Windows)** : Si vous êtes sous Windows, vous pouvez utiliser Task Scheduler pour planifier l’exécution automatique de votre script ETL.

### Orchestration avec Apache Airflow :  
_ Utilisez **Apache Airflow** pour gérer l'exécution périodique de votre ETL et orchestrer les tâches. Airflow offre une interface graphique pour gérer les workflows et permet de suivre les exécutions passées.  
_ Créez un **DAG (Directed Acyclic Graph)** pour définir votre pipeline ETL et configurez l'intervalle de déclenchement pour chaque heure.  

__Exemple de code Airflow pour déclencher l’ETL chaque heure :
```python
from airflow import DAG
from airflow.operators.python_operator import PythonOperator
from datetime import datetime, timedelta

# Définir les paramètres du DAG
default_args = {
    'owner': 'user',
    'start_date': datetime(2023, 9, 1),
    'retries': 1,
    'retry_delay': timedelta(minutes=5),
}

# Créer le DAG
dag = DAG(
    'etl_hourly',
    default_args=default_args,
    schedule_interval='0 * * * *',  # Déclenchement toutes les heures
)

# Fonction à exécuter
def run_etl():
    # Importer et exécuter votre script ETL
    import your_etl_script
    your_etl_script.run_etl()

# Opérateur pour déclencher l'ETL
etl_task = PythonOperator(
    task_id='run_etl',
    python_callable=run_etl,
    dag=dag
)

```

_ Ce DAG sera automatiquement déclenché toutes les heures grâce à ```schedule_interval='0 * * * *'.```  

### 2.Orchestration avec Apache Airflow :  

_ Utilisez Apache Airflow pour gérer l'exécution périodique de votre ETL et orchestrer les tâches. Airflow offre une interface graphique pour gérer les workflows et permet de suivre les exécutions passées.  
_ Créez un DAG (Directed Acyclic Graph) pour définir votre pipeline ETL et configurez l'intervalle de déclenchement pour chaque heure.
_ Exemple de code Airflow pour déclencher l’ETL chaque heure :  

``` python
from airflow import DAG
from airflow.operators.python_operator import PythonOperator
from datetime import datetime, timedelta

# Définir les paramètres du DAG
default_args = {
    'owner': 'user',
    'start_date': datetime(2023, 9, 1),
    'retries': 1,
    'retry_delay': timedelta(minutes=5),
}

# Créer le DAG
dag = DAG(
    'etl_hourly',
    default_args=default_args,
    schedule_interval='0 * * * *',  # Déclenchement toutes les heures
)

# Fonction à exécuter
def run_etl():
    # Importer et exécuter votre script ETL
    import your_etl_script
    your_etl_script.run_etl()

# Opérateur pour déclencher l'ETL
etl_task = PythonOperator(
    task_id='run_etl',
    python_callable=run_etl,
    dag=dag
)
```  

_ Ce DAG sera automatiquement déclenché toutes les heures grâce à ```schedule_interval='0 * * * *'.```  

### 3.Utilisation de Kubernetes CronJobs :  
_ Si vous travaillez dans un environnement Kubernetes, configurez un CronJob pour exécuter le script ETL toutes les heures dans un pod Kubernetes.  
_ Exemple de configuration d'un CronJob YAML pour Kubernetes :  
```yaml
apiversion: batch/v1
kind: CronJob
metadata:
  name: etl-hourly
  spec:  schedule: "0 * * * *" #Chaque heure
    jobTemplate:
      template:
        spec:
          containers:
          name:etljob
          image:python:3.9
          command:[python,"/path/to/your_etl_script.py"]
        restartPolicy: OnFailure
``` 

_ Le CronJob exécutera automatiquement le script ETL à l'intervalle spécifié et dans un environnement conteneurisé, assurant une exécution isolée et scalable.

## 4.Surveillance des Jobs et Alertes :  
**Logs et Monitoring :**  
_ Capturez les logs d’exécution pour chaque déclenchement dans des fichiers log ou dans un système de gestion des logs centralisé (comme ELK ou Graylog).  
_ Surveillez les erreurs, les échecs, et le temps d’exécution à l’aide de systèmes de monitoring comme Prometheus ou Grafana. Vous pouvez aussi utiliser les dashboards d’Airflow pour suivre les exécutions.  

**Alertes en cas d’échec :**  
_ Configurez des alertes par e-mail ou via des outils comme Slack ou PagerDuty pour recevoir une notification instantanée en cas de panne ou d’échec du job ETL.  
_ Dans Airflow, vous pouvez ajouter des notifications dans les default_args avec email_on_failure et email_on_retry.  

## 5.Scalabilité et Optimisation :  
_ Si vous anticipez une augmentation du volume de données, assurez-vous que votre infrastructure supporte la charge. Utilisez des instances cloud (comme AWS, GCP) capables de se scaler dynamiquement.  
_ Optimisez les étapes de transformation et de chargement de votre pipeline pour réduire le temps d'exécution et garantir que le processus ETL soit terminé avant la prochaine exécution horaire.  

## 6.Tests et Maintenance :    
_ Effectuez des tests réguliers de vos jobs ETL pour identifier des goulots d’étranglement ou des risques de défaillance à mesure que les volumes de données augmentent.  
_ Préparez un plan de maintenance pour surveiller l’évolution des performances du système et ajuster les paramètres si nécessaire (par exemple, ajuster les intervalles de déclenchement ou les ressources allouées).  

## 7.Versioning du Code :  
_ Utilisez un système de contrôle de version comme **Git** pour gérer les modifications du code ETL.  
_ Déployez de nouvelles versions avec un pipeline CI/CD (comme **GitLab CI**, **Jenkins** ou **GitHub Actions**) qui intègre des tests automatiques et déploie les modifications en production en toute sécurité.

