# Projet RabbitMQ - Infrastructure pour MSPR

Ce dépôt contient la configuration pour exécuter un conteneur RabbitMQ via Docker, ainsi qu'une procédure d'installation pour les différentes API de notre projet MSPR : Clients, Produits, et Commandes. 

## Pré-requis

- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)

## Initialisation

1. **Créer le réseau Docker partagé** :  
   Pour permettre la communication entre RabbitMQ et les API, il est nécessaire de créer un réseau nommé `backend`.

   ```bash
   docker network create backend
   ```

2. **Cloner les dépôts des API** :

   Pour obtenir et configurer les APIs, clonez les dépôts suivants :

   - [API Clients](https://github.com/Cortexico/MSPR-API-Clients.git)
   - [API Produits](https://github.com/Cortexico/MSPR-API-Produits.git)
   - [API Commandes](https://github.com/Cortexico/MSPR-API-Commandes.git)

   ```bash
   git clone https://github.com/Cortexico/MSPR-API-Clients.git
   git clone https://github.com/Cortexico/MSPR-API-Produits.git
   git clone https://github.com/Cortexico/MSPR-API-Commandes.git
   ```

## Lancer RabbitMQ

Une fois le réseau `backend` créé, exécutez le conteneur RabbitMQ en arrière-plan :

```bash
docker-compose -f docker-compose.rabbitmq.yml up -d
```

- Interface de gestion : [http://localhost:15672](http://localhost:15672)  
  - Utilisateur : `guest`
  - Mot de passe : `guest`

## Lancer les API

Chaque API possède sa propre procédure de lancement. Depuis le dossier de chaque API, lancez :

```bash
docker-compose up --build
```

### Liens directs vers les API :

- **API Clients** : [Documentation et Procédure](https://github.com/Cortexico/MSPR-API-Clients)
- **API Produits** : [Documentation et Procédure](https://github.com/Cortexico/MSPR-API-Produits)
- **API Commandes** : [Documentation et Procédure](https://github.com/Cortexico/MSPR-API-Commandes)


Parfait, voici une **explication simple à ajouter dans le README** (dans la section Kubernetes par exemple), comme pour les autres APIs :

---

### Fichiers ajoutés pour Kubernetes

Pour permettre le déploiement de RabbitMQ dans un cluster Kubernetes, les fichiers suivants ont été ajoutés :

- `rabbitmq-deployment.yaml` : Déploie un conteneur RabbitMQ avec l’image officielle `rabbitmq:3-management`, incluant l’interface web d’administration.
- `rabbitmq-service.yaml` : Crée un service de type `NodePort` pour exposer RabbitMQ à l’extérieur du cluster :
  - Port **5672** : utilisé pour les communications AMQP entre services.
  - Port **15672** : permet d’accéder à l’interface d’administration Web RabbitMQ.

### Exemple de commande de déploiement :
```bash
kubectl apply -f rabbitmq-deployment.yaml
kubectl apply -f rabbitmq-service.yaml
```

Une fois déployé, l’interface web est accessible à l’adresse :
```bash
http://<minikube_ip>:<nodePort>
```
avec les identifiants :
```
Username: guest
Password: guest
```