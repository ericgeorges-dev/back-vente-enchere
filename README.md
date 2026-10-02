# 🔨 Vente aux enchères – API Backend

API REST Java / Spring Boot d'une plateforme de **vente aux enchères en ligne** : gestion des clients,
des enchères, des offres et des soldes, avec un back-office d'administration.

> Projet réalisé dans un cadre académique (projet cloud). Interface web : [S5-Projet-Rojo-FrontEnchereCloud](https://github.com/ericgeorges-dev/S5-Projet-Rojo-FrontEnchereCloud)

## ✨ Fonctionnalités

### Back-office (administrateur)
- Authentification de l'administrateur
- CRUD des catégories de produits (musique, art, moto, voiture, football, …)
- Statistiques : catégories les plus populaires, enchères les mieux vendues, meilleurs acheteurs
- Validation des rechargements de compte (dépôts / retraits)
- Calcul automatique de la fin d'une enchère à partir de sa durée

### Front-office (clients)
- Liste des enchères par statut (en cours, à venir, terminées) et fiche détaillée
- Recherche avancée multicritère (requêtes SQL générées dynamiquement)
- Dépôt d'offres sur une enchère
- Historique des enchères et des offres d'un client
- Gestion du solde (dépôt, retrait)
- Notifications (stockées dans MongoDB)

## 🛠️ Technologies
| Domaine | Outils |
|---|---|
| Langage | Java 17 |
| Framework | Spring Boot 3.0.1 (Web, Data JPA, Data JDBC) |
| Base relationnelle | PostgreSQL |
| Base NoSQL | MongoDB (notifications) |
| Build | Maven (wrapper inclus) |
| Déploiement | Railway |

## 🗄️ Modèle de données (PostgreSQL)
`admin`, `client`, `categorie`, `enchere`, `offre`, `vendu`, `solde`, `mouvementSolde`, `token`, `token_user`

- Une **enchère** appartient à un client (vendeur) et à une catégorie.
- Une **offre** relie un client à une enchère avec un montant.
- Une ligne **vendu** désigne l'offre gagnante d'une enchère.
- Les **tokens** authentifient les administrateurs et les clients.

Le script de création est dans [`src/main/scripts/base.sql`](src/main/scripts/base.sql).

## 🧱 Architecture
```
src/main/java/com/enchere/
├── config/base/      Configuration PostgreSQL et MongoDB
├── controllers/      Admin, Categorie, Client, Enchere, Offre, Solde
├── postgres/         Modèles et repositories (PostgreSQL)
├── mongos/           Modèles et repositories (MongoDB)
├── helper/ utils/    Séquences, accès base, utilitaires
└── org/gen/dao/      DAO générique basé sur des annotations
```

## 🚀 Lancer le projet

### Prérequis
Java 17, Maven (ou le wrapper `mvnw`), PostgreSQL, MongoDB.

### Installation
```bash
git clone https://github.com/ericgeorges-dev/back-vente-enchere.git
cd back-vente-enchere
```

1. Créez une base PostgreSQL, puis exécutez `src/main/scripts/base.sql`.
2. Copiez `src/main/resources/application.properties.example` vers `application.properties`
   et renseignez vos propres identifiants (**ne les publiez jamais sur GitHub**).
3. Démarrez l'application :
```bash
./mvnw spring-boot:run
```

L'API est disponible sur `http://localhost:8080/api/projetEnchere`.

## 🔌 Principales routes
| Ressource | Rôle |
|---|---|
| `/admin` | Connexion de l'administrateur |
| `/categorie` | CRUD des catégories |
| `/client` | Inscription et connexion des clients |
| `/enchere` | Liste, détail, création, recherche |
| `/enchere/encherir` (POST) | Placer une offre |
| `/solde` | Rechargement et validation de solde |

## 📌 État du projet
- ✅ Backend back-office et front-office
- ⏳ Notifications de fin d'enchère à finaliser
- ⏳ Pages d'interface (voir le dépôt front)

## 👤 Auteur
**Eric Georges Lova** – [GitHub](https://github.com/ericgeorges-dev)
