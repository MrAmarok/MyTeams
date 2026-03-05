# MyTeams 💬

![Language](https://img.shields.io/badge/Language-C-blue.svg)
![Build](https://img.shields.io/badge/Build-Make-success.svg)

**MyTeams** est un projet EPITECH de la PROMO 2027 où le but est de reproduire le fonctionnement de Teams 

Ce projet repose sur une architecture **Client/Serveur** via des **Sockets TCP** en langage C. Il permet à plusieurs utilisateurs de se connecter simultanément, de discuter en privé, de créer des équipes, des canaux de discussion et des fils de messages (threads).


## 🏗️ Architecture du Projet

Le dépôt est divisé en plusieurs composants principaux :

* `server/` : Code source du serveur. Il gère les connexions entrantes, stocke les données (utilisateurs, équipes, messages) et diffuse les informations.
* `client/` : Code source du client interactif permettant aux utilisateurs d'envoyer des commandes au serveur.
* `lib/my/` : Bibliothèque contenant des fonctions utilitaires de base en C.
* `libs/myteams/` : Bibliothèque dynamique fournie pour la journalisation des événements (logs).
* `protocol.txt` : Documentation du protocole de communication custom mis en place entre le client et le serveur.
* `help.txt` : Fichier de documentation pour les commandes disponibles.


## ⚙️ Prérequis et Compilation

### Prérequis
* Un système d'exploitation basé sur UNIX (Linux, macOS).
* Le compilateur `gcc`.
* L'outil `make`.

### Compilation

À la racine du projet, utilisez le `Makefile` pour compiler l'ensemble des programmes :

```bash
make
```

Cela générera généralement deux exécutables :

* `myteams_server` (le serveur)
* `myteams_cli` (le client)

Pour nettoyer les fichiers de compilation (`.o`) :

```bash
make clean
```

Pour tout nettoyer (fichiers objets + exécutables) :

```bash
make fclean
```

## 🚀 Utilisation

### 1. Lancer le Serveur

Le serveur doit toujours être lancé en premier. Il écoute sur un port spécifique.

```bash
./myteams_server [port]
```

* **port** : Le numéro du port sur lequel le serveur va écouter les connexions entrantes (ex: `8080`).

### 2. Lancer le Client

Dans un autre terminal (ou sur une autre machine), lancez le client pour vous connecter au serveur.

```bash
./myteams_cli [ip] [port]
```

* **ip** : L'adresse IP du serveur (utilisez `127.0.0.1` si le serveur tourne sur la même machine).
* **port** : Le même port que celui spécifié lors du lancement du serveur.



## 🛠️ Fonctionnalités & Commandes

Une fois le client connecté, l'utilisateur peut interagir avec le serveur via une série de commandes. Vous pouvez consulter les détails complets en tapant `/help` (référencé par `help.txt`).

Voici les actions principales :

* **Authentification** :
* `/login ["username"]` : Se connecter au serveur.
* `/logout` : Se déconnecter.


* **Informations** :
* `/users` : Liste tous les utilisateurs enregistrés.
* `/user ["user_uuid"]` : Affiche les informations d'un utilisateur spécifique.


* **Messagerie Privée** :
* `/send ["user_uuid"] ["message"]` : Envoie un message privé à un utilisateur.
* `/messages ["user_uuid"]` : Affiche l'historique des messages échangés avec un utilisateur.


* **Environnement Collaboratif** :
* `/create` : Crée une équipe, un canal ou un thread (selon le contexte actuel).
* `/list` : Liste les équipes, les canaux ou les threads existants.
* `/info` : Affiche les détails de l'élément actuel.
* `/use ?["team_uuid"] ?["channel_uuid"] ?["thread_uuid"]` : Change le contexte actuel pour naviguer dans l'arborescence (Équipe > Canal > Thread).
* `/subscribe ["team_uuid"]` : S'abonner à une équipe.
* `/subscribed ?["team_uuid"]` : Liste les équipes auxquelles vous êtes abonné, ou les abonnés d'une équipe.


## 📡 Protocole de Communication

Le serveur et le client communiquent via un protocole textuel/binaire spécifique (requêtes et réponses formatées).
Les codes de retour ou le format des trames sont définis de manière stricte.

👉 *Pour plus de détails sur le format des paquets réseau, veuillez consulter le fichier `protocol.txt` présent à la racine du dépôt.*
