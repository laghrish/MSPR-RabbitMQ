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
