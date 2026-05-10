================================================================================
                    APPLICATION WEB JEE - GESTION DES PRODUITS
                         Projet : jee-jsp-p1 | Java EE + JSP
================================================================================

------------------------------------------------------------------------
DESCRIPTION GENERALE
------------------------------------------------------------------------

Cette application est une application web Java EE (Jakarta EE) qui permet
la navigation et la gestion d'un catalogue de produits. Elle est construite
selon le patron de conception MVC (Modèle - Vue - Contrôleur) en utilisant
les Servlets Java comme contrôleurs et les pages JSP comme vues.

L'application tourne sur un serveur Tomcat 7 embarqué via Maven et ne
nécessite pas de base de données externe : les données sont stockées en
mémoire (in-memory) pendant l'exécution.

------------------------------------------------------------------------
FONCTIONNALITES ACTUELLES (application complète)
------------------------------------------------------------------------

  [OK]  Affichage de la liste des produits (navigation catalogue)
  [OK]  Création d'un nouveau produit via un formulaire HTML
  [OK]  Suppression d'un produit depuis la liste
  [EN COURS]  Authentification des utilisateurs (login / inscription)

------------------------------------------------------------------------
ARCHITECTURE DU PROJET (MVC)
------------------------------------------------------------------------

  src/main/java/org/example/
  │
  ├── models/
  │   ├── Product.java           → Modèle : représente un produit
  │   │                            Champs : id, name, description,
  │   │                                     price, quantity, category
  │   └── ProductCategory.java   → Enum des catégories disponibles :
  │                                ELECTRONICS, CLOTHING, HOME, BEAUTY,
  │                                SPORTS, TOYS, BOOKS, FOOD, AUTOMOTIVE, OTHER
  │
  ├── dao/
  │   └── ProductMemoryDB.java   → Couche d'accès aux données (DAO)
  │                                Stockage en mémoire avec une liste statique
  │                                Opérations : add(), findAll(), delete()
  │
  ├── controllers/
  │   ├── ProductListServlet.java    → GET /products
  │   │                               Récupère tous les produits et les
  │   │                               transmet à products.jsp via RequestDispatcher
  │   ├── ProductCreateServlet.java  → POST /product/create
  │   │                               Reçoit les données du formulaire,
  │   │                               crée un Product et l'enregistre en mémoire
  │   └── ProductDeleteServlet.java  → GET /product/delete?id=...
  │                                   Supprime un produit par son identifiant
  │
  └── Main.java                  → Classe principale (point d'entrée)

  src/main/webapp/
  ├── index.html                 → Page d'accueil de l'application
  ├── createProduct.html         → Formulaire de création d'un produit
  ├── products.jsp               → Vue JSP : affichage du catalogue produits
  └── WEB-INF/
      └── web.xml                → Descripteur de déploiement de l'application

------------------------------------------------------------------------
CONCEPTS TECHNIQUES UTILISES
------------------------------------------------------------------------

  - Java EE / Servlet API 3.0    : gestion des requêtes HTTP (GET, POST)
  - JSP (JavaServer Pages)       : génération dynamique des vues HTML
  - Pattern MVC                  : séparation des responsabilités
  - DAO (Data Access Object)     : abstraction de la couche données
  - Lombok                       : génération automatique des getters/setters
  - Maven + Tomcat7 Plugin       : build et déploiement simplifié
  - Annotations @WebServlet      : mapping des URL sans configuration XML
  - RequestDispatcher            : transfert de la requête vers la JSP
  - AtomicLong                   : génération d'IDs thread-safe

------------------------------------------------------------------------
FLUX DE NAVIGATION
------------------------------------------------------------------------

  Page d'accueil (index.html)
       │
       ├──> [Voir les produits]  ──>  GET /products
       │                                   │
       │                           ProductListServlet
       │                                   │
       │                           products.jsp (affichage du tableau)
       │                                   │
       │                    ┌──────────────┴──────────────┐
       │                    │                             │
       │              [Supprimer]                  [Ajouter un produit]
       │           GET /product/delete          createProduct.html
       │                    │                             │
       │           ProductDeleteServlet           POST /product/create
       │                    │                             │
       └────────────────────┴── Redirection vers /products ───────────┘

------------------------------------------------------------------------
LANCER L'APPLICATION
------------------------------------------------------------------------

  Prérequis :
    - Java 8+
    - Maven installé

  Commande :
    mvn tomcat7:run

  Accès dans le navigateur :
    http://localhost:8082/SampleServlet/

------------------------------------------------------------------------
ETAT D'AVANCEMENT
------------------------------------------------------------------------

  >> FONCTIONNALITE EN COURS DE DEVELOPPEMENT :

     Authentification des utilisateurs

     Cette fonctionnalité est actuellement en cours d'implémentation.
     Elle comprendra :
       - Un formulaire d'inscription (nom, email, mot de passe)
       - Un formulaire de connexion
       - La gestion des sessions utilisateur (HttpSession)
       - La protection des pages (redirection si non connecté)
       - Un modèle User et un DAO UserMemoryDB associé

     Une fois terminée, l'accès à la liste et à la gestion des produits
     sera réservé aux utilisateurs authentifiés.

------------------------------------------------------------------------
TECHNOLOGIES
------------------------------------------------------------------------

  Langage          : Java 8
  Framework        : Java EE (Servlets / JSP)
  Build            : Maven
  Serveur          : Apache Tomcat 7 (plugin Maven)
  Bibliothèques    : Lombok 1.18.28
  Packaging        : WAR (Web Application Archive)

------------------------------------------------------------------------
AUTEUR
------------------------------------------------------------------------

  Projet académique - En cours de développement
  Dépôt GitHub : [à compléter]

================================================================================
