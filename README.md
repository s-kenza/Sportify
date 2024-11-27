# Sportify - Un simple E-commerce avec Nodejs

## Fonctionnalités

- Cette application d'e-commerce est créée avec Nodejs, Expressjs, Mongodb, Vuejs et TailwindCSS.
- 3 rôles : admin, vendeur et utilisateur.
- L'administrateur peut créer, afficher, mettre à jour et supprimer des catégories. Il peut afficher et supprimer des utilisateurs, des boutiques, des produits et des avis.
- Les vendeurs peuvent créer, afficher, mettre à jour et supprimer une boutique (une seule) et des produits.
- Les utilisateurs peuvent postuler pour devenir vendeurs. Ils peuvent parcourir les boutiques et les produits, créer et mettre à jour leur profil, ainsi que créer et supprimer des avis.

## A faire

- Panier d'achat
- Refonte du dashboard de l'admin
- Système d'évaluation/d'évaluation des produits

## Instructions d'installation

Cloner ce projet avec la commande suivante :

```bash
git clone https://github.com/ericnanhu/ecommerce-nodejs.git
```

Ouvrir le projet avec un éditeur de coder et passer au dossier **backend**:

```bash
cd backend
```

Installer les dépendances :

```bash
npm install
```

Lancer docker compose pour démarrer la base de données :

```bash
docker-compose up
```

Démarrer le back :

```bash
npm run watch
```

Se déplacer dans le dossier **frontend** et installer les dépendances :

```bash
npm install
```

Démarrer le front :

```bash
npm run dev
```