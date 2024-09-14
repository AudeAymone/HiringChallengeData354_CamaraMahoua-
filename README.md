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
Aussi, il est important de notifier que superset n'interagit pas nativement avec des données non relationnelles. Pour ce faire, nous avons installé apache drill qui représente une passerelle entre Apache Superset et MongoDb. Cliquez sur [ce lien](https://medium.com/@thoren.lederer/query-data-from-mongodb-in-apache-superset-with-the-help-of-apache-drill-full-tutorial-b34c33eac6c1) afin d'avoir toute la docummentation requise pour l'installation et le lien avec Apache Superset.

Pour notre part, nous avons rencontré des problèmes au niveau de la connexion de Apache Drill et Apache Superset.  
Voici les captures qui attestent du niveau atteint:  


![Apache Drill](https://github.com/AudeAymone/HiringChallengeData354_CamaraMahoua-/blob/main/Images%20superset/Apache%20Drill.png)  


![Apache Superset Erreur](https://github.com/AudeAymone/HiringChallengeData354_CamaraMahoua-/blob/main/Images%20superset/Apache_Superset_Error.png)  


**Nous en appelons à votre amabilité, afin que, peu importe la finalité du Hiring Challenge, nous puissions avoir un exemple de bonne démarche à suivre pour nos projets futurs.  Merci de votre compréhension**

## Modèle de prediction  
Pour le modèle de prédiction, nous avons choisi Tensorflow puisque nous l'avons déjà utilisé auparant pour d'autres projets.  
Toutefois, les modèles de machine learning tels que ARIMA ou Prophet étaient tous aussi valables.  
Voir [DataTreatment.ipynb](https://github.com/AudeAymone/HiringChallengeData354_CamaraMahoua-/blob/main/DataTreatment.ipynb).    

## Stratégie de mise en production du ETL  

### 1.Préparation au déploiement :  
#### Tests Locaux  
_ **Validation du Code**: Assurez-vous que l'ETL fonctionne correctement sur votre environnement de développement local.    
_ **Validation des Visualisations**: Testez les visualisations et dashboards dans Superset pour vérifier que les données sont correctes et que les performances sont acceptables..  

#### Environnement de Préproduction: 
_ **Configuration:**: Créez un environnement de préproduction qui imite la production pour tester les déploiements avant de passer en production.   
_ **Tests de Charge**: Effectuez des tests de charge pour évaluer la performance de votre ETL et de vos dashboards sous des conditions de charge élevée.  


### 2.Déploiement du ETL :  
#### Automatisation 
_ **CI/CD**: Mettez en place des pipelines CI/CD (Intégration Continue/Déploiement Continu) pour automatiser les déploiements de votre ETL et des configurations de Superset.     
_ **Scripts de Déploiement**: Écrivez des scripts pour déployer l'ETL, mettre à jour les configurations de Superset, et appliquer les migrations de base de données.  

#### Conteneurisation: 
_ **Docker**:  Utilisez Docker pour empaqueter votre ETL et Superset afin de garantir une consistance entre les environnements de développement, de préproduction et de production.   
_ **Tests de Charge**: Effectuez des tests de charge pour évaluer la performance de votre ETL et de vos dashboards sous des conditions de charge élevée.  

#### Configuration: 
_ **Variables d'Environnement**:  Configurez les variables d'environnement pour les connexions de base de données, les clés API, et les autres paramètres nécessaires.  
_ **Fichiers de Configuration**: Assurez-vous que les fichiers de configuration pour l'ETL et Superset sont correctement configurés pour l'environnement de production.  


### 3.Surveillance et Gestion:  
#### Monitoring 
_ **Logs**: Configurez la collecte des logs pour surveiller les erreurs et les anomalies dans l'ETL et Superset.      
_ **Alertes**: Configurez des alertes pour les erreurs critiques, les pannes ou les problèmes de performance.  

#### Sauvegardes: 
_ **Données**: Mettez en place des sauvegardes régulières pour les bases de données et les fichiers de configuration.  
_ **Scripts**: Assurez-vous que les scripts ETL sont également sauvegardés et versionnés.   


### 4.Maintenance:
#### Mises à Jour
_ **ETL**: Planifiez des mises à jour régulières pour améliorer les fonctionnalités et corriger les bugs.     
_ **Superset**: Mettez à jour Superset avec les dernières versions pour bénéficier des nouvelles fonctionnalités et correctifs de sécurité.  

#### Optimisation: 
_ **Performance**: Surveillez les performances de l'ETL et des dashboards pour identifier et résoudre les goulets d'étranglement.   
_ **Scalabilité**: Ajustez les ressources (CPU, RAM) en fonction de la charge et des besoins de votre ETL et Superset.     

### 5.Documentation et Formation:  
#### Documentation
_ **Processus**: Documentez le processus de déploiement, y compris les étapes, les configurations et les dépendances.   
_ **Résolution des Problèmes**: Créez une documentation sur la résolution des problèmes courants et les étapes de dépannage.  

#### Formation (Facultatif): 
_ **Équipe**: Formez les membres de l'équipe sur l'utilisation des outils relatifs à notre ETL et Superset, ainsi que sur les procédures de maintenance et de dépannage.  
     

### 6. Sécurité:  
#### Contrôle d'Accès
_ **Permissions**: Configurez les contrôles d'accès et les permissions dans Superset pour garantir que seules les personnes autorisées peuvent accéder aux données sensibles.   

#### Cryptage: 
_ **Données**: Assurez-vous que les données sensibles sont cryptées en transit et au repos.  


## Stratégie de déclenchement du ETL automatiquement chaque heure  

### 1.Utilisation de Cron Jobs:    
#### Configuration sur un Serveur Linux Tests Locaux  
**Créer un Script d'Exécution**: Écrivez un script shell ou Python pour exécuter votre ETL. Assurez-vous qu'il est exécutable.   
 
```bash
#!/bin/bash
/usr/bin/python3 /chemin/vers/votre_script_etl.py
```

**Configurer Cron Job**  
_Ouvrez le fichier de configuration des tâches cron avec la commande suivante:   
```bash
crontab -e
```  
_Ajoutez une ligne pour exécuter le script toutes les heures :  
```bash
0 * * * * /chemin/vers/votre_script.sh
```  

#### Configuration sur windows:  
**Créer un Script d'Exécution**  
_ Écrivez un script batch (.bat) pour exécuter votre ETL.  
```bash
@echo off
python C:\chemin\vers\votre_script_etl.py
```    

**Configurer le Planificateur de Tâches**    
_ Ouvrez le Planificateur de Tâches et créez une nouvelle tâche.    
_  Définissez le déclencheur pour exécuter la tâche toutes les heures.   
_ Définissez l'action pour exécuter le script batch que vous avez créé.  
    

### 2.Utilisation de Docker avec Cron:   
#### Dockerfile avec Cron  
**Créer un Dockerfile**  
_ Configurez un Dockerfile pour installer cron et définir les tâches.  
``` Dockerfile
FROM python:3.9-slim

# Installer cron
RUN apt-get update && apt-get install -y cron

# Copier le script ETL et les fichiers de cron
COPY votre_script_etl.py /usr/local/bin/votre_script_etl.py
COPY crontab /etc/cron.d/mon_cron

# Donner les permissions nécessaires
RUN chmod 0644 /etc/cron.d/mon_cron

# Appliquer les fichiers de cron
RUN crontab /etc/cron.d/mon_cron

# Exposer le port et démarrer cron
CMD ["cron", "-f"]
```

**Créer un fichier Crontab**  
_ Créez un fichier crontab avec la configuration suivante:  
``` bash
# Exécuter le script toutes les heures
0 * * * * /usr/bin/python3 /usr/local/bin/votre_script_etl.py
```

**Déploiement Docker**  
_ Construisez et exécutez votre conteneur Docker :  
``` bash
docker build -t mon_etl .
docker run -d mon_etl
```

### 3.Utilisation d'Apache Airflow  
#### Configurer un DAG  
**Créer un DAG pour l'ETL** 
_ Écrivez un fichier Python pour définir un DAG dans Airflow.  
```python
from airflow import DAG
from airflow.operators.python_operator import PythonOperator
from airflow.utils.dates import days_ago
import subprocess

def run_etl():
    subprocess.run(["python3", "/chemin/vers/votre_script_etl.py"])

default_args = {
    'owner': 'airflow',
    'depends_on_past': False,
    'email_on_failure': False,
    'email_on_retry': False,
    'retries': 1,
    'retry_delay': timedelta(minutes=5),
}

dag = DAG(
    'etl_dag',
    default_args=default_args,
    description='Un DAG pour exécuter l\'ETL chaque heure',
    schedule_interval='@hourly',
    start_date=days_ago(1),
    catchup=False,
)

t1 = PythonOperator(
    task_id='run_etl',
    python_callable=run_etl,
    dag=dag,
)
```
**Déployer Airflow**  
_ Déployez Apache Airflow en utilisant Docker, Kubernetes ou directement sur un serveur.  

### 4.Utilisation de Cloud Providers  
#### AWS Lambda avec CloudWatch Events  
**Créer une Fonction Lambda**  
_ Écrivez une fonction Lambda pour exécuter votre ETL.  
**Configurer CloudWatch Events**  
_ Configurez une règle CloudWatch Events pour déclencher la fonction Lambda toutes les heures.  
#### Google Cloud Functions avec Cloud Scheduler  
**Créer une Fonction Cloud**  
_ Écrivez une fonction Cloud pour exécuter votre ETL.  
**Configurer Cloud Scheduler**  
_ Configurez Cloud Scheduler pour déclencher la fonction Cloud toutes les heures.  

### Surveillance et Gestion  
**Logs**: Assurez-vous que les logs de votre ETL sont capturés pour surveiller les erreurs et les performances.  
**Alertes**: Configurez des alertes pour les échecs d'exécution ou les problèmes de performance.  

