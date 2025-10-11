# Chapitre 0 : Découverte de Git avec GitHub Desktop

- [Chapitre 0 : Découverte de Git avec GitHub Desktop](#chapitre-0--découverte-de-git-avec-github-desktop)
  - [Objectifs du module](#objectifs-du-module)
- [Introduction à Git et GitHub](#introduction-à-git-et-github)
  - [Qu’est-ce que Git ?](#quest-ce-que-git-)
  - [Qu’est-ce que GitHub ?](#quest-ce-que-github-)
- [Créer un dépôt sur GitHub](#créer-un-dépôt-sur-github)
  - [Étape 1 – Créer un compte GitHub](#étape-1--créer-un-compte-github)
  - [Étape 2 – Créer un dépôt (repository)](#étape-2--créer-un-dépôt-repository)
- [Cloner et gérer le dépôt avec GitHub Desktop](#cloner-et-gérer-le-dépôt-avec-github-desktop)
  - [Étape 1 – Installer GitHub Desktop](#étape-1--installer-github-desktop)
  - [Étape 2 – Cloner votre dépôt sur votre ordinateur](#étape-2--cloner-votre-dépôt-sur-votre-ordinateur)
  - [Étape 3 – Modifier un fichier et créer un commit](#étape-3--modifier-un-fichier-et-créer-un-commit)
  - [Étape 4 – Envoyer (push) les modifications sur GitHub](#étape-4--envoyer-push-les-modifications-sur-github)
- [Travailler avec des branches](#travailler-avec-des-branches)
  - [Étape 1 – Créer une branche](#étape-1--créer-une-branche)
  - [Étape 2 – Modifier et valider](#étape-2--modifier-et-valider)
  - [Étape 3 – Fusionner la branche (merge)](#étape-3--fusionner-la-branche-merge)
- [Collaborer à plusieurs sur un projet](#collaborer-à-plusieurs-sur-un-projet)
- [Récapitulatif visuel du workflow GitHub Desktop](#récapitulatif-visuel-du-workflow-github-desktop)
- [Conseils et bonnes pratiques](#conseils-et-bonnes-pratiques)
- [À retenir](#à-retenir)
- [Liens utiles](#liens-utiles)


## Objectifs du module

Voici les objectifs de ce TP :
- [x] Créer un compte GitHub
- [x] Créer un dépôt (repository) en ligne sur GitHub
- [x] Gérer un projet localement avec GitHub Desktop
- [x] Comprendre les notions de commit, branche et synchronisation
- [x] Travailler en équipe sans ligne de commande

# Introduction à Git et GitHub

## Qu’est-ce que Git ?

Git est un **outil de suivi des versions**.  
Il permet de sauvegarder l’historique des modifications d’un projet (fichiers, code, documentation, etc.).  
Chaque enregistrement s’appelle un **commit**.

## Qu’est-ce que GitHub ?

GitHub est une **plateforme en ligne** qui héberge vos projets Git.  
C’est l’endroit où vous allez **collaborer**, **sauvegarder** et **partager** vos dépôts (repositories).

# Créer un dépôt sur GitHub

## Étape 1 – Créer un compte GitHub

1. Rendez-vous sur [https://github.com](https://github.com)  
2. Cliquez sur **Sign up**  
3. Entrez un identifiant, un email et un mot de passe  
4. Vérifiez votre adresse e-mail

## Étape 2 – Créer un dépôt (repository)

1. Une fois connecté, cliquez sur le bouton **New repository** (en haut à gauche ou sur votre page d’accueil)  
2. Remplissez :
   - **Repository name** : mon-premier-projet  
   - **Description** : Mon premier dépôt GitHub  
   - **Visibility** : cochez *Public*  
   - Cochez **Add a README file** (important !)  
3. Cliquez sur **Create repository**

Vous venez de créer votre premier dépôt GitHub !  
Il contient un fichier *README.md* qui décrit votre projet.

# Cloner et gérer le dépôt avec GitHub Desktop

## Étape 1 – Installer GitHub Desktop

1. Allez sur [https://desktop.github.com](https://desktop.github.com)  
2. Téléchargez et installez l’application  
3. Connectez-vous avec votre compte GitHub


## Étape 2 – Cloner votre dépôt sur votre ordinateur

1. Ouvrez **GitHub Desktop**  
2. Cliquez sur **File → Clone repository**  
3. Sélectionnez votre dépôt *mon-premier-projet*  
4. Choisissez un dossier local (ex. Documents/GitHub)  
5. Cliquez sur **Clone**

:bulb: GitHub Desktop crée une **copie locale** de votre projet GitHub sur votre ordinateur.

## Étape 3 – Modifier un fichier et créer un commit

1. Ouvrez le dossier cloné sur votre ordinateur  
2. Ouvrez le fichier *README.md* et ajoutez une ligne, par exemple :
   > Ceci est mon premier test avec GitHub Desktop.
3. Revenez sur GitHub Desktop : la modification apparaît en bas à gauche
4. Saisissez un message de commit, par exemple :
   > Ajout d’une première description dans README.md
5. Cliquez sur **Commit to main**

:bulb: Vous venez d’enregistrer une **version** de votre projet.

## Étape 4 – Envoyer (push) les modifications sur GitHub

1. Cliquez sur le bouton **Push origin** en haut de GitHub Desktop  
2. Allez sur [github.com](https://github.com)  
3. Rechargez la page de votre dépôt  
✅ Vous voyez votre modification en ligne !

# Travailler avec des branches

Les **branches** permettent de travailler sur une nouvelle idée sans modifier la version principale du projet.

## Étape 1 – Créer une branche

1. Dans GitHub Desktop, cliquez sur le menu **Current Branch → New Branch**  
2. Nommez-la par exemple *nouvelle-fonctionnalite*  
3. Cliquez sur **Create branch**

## Étape 2 – Modifier et valider

1. Modifiez à nouveau *README.md* (par exemple, ajoutez une nouvelle ligne de texte)  
2. Revenez sur GitHub Desktop  
3. Ajoutez un message de commit :
   > Ajout d’une section sur la nouvelle fonctionnalité
4. Cliquez sur **Commit to nouvelle-fonctionnalite**
5. Cliquez sur le bouton **Push origin** en haut de GitHub Desktop  

## Étape 3 – Fusionner la branche (merge)

Nous allons créer la merge request via l’interface web de GitHub.

1. Dans GitHub : New Pull Request → base = main, compare = develop
2. Clique sur Create Pull Request 
3. Regarder les changements, s'il n'y a pas de conflit
4. Merger pour valider la Pull Request

:bulb: Votre travail de la branche a été fusionné dans la version principale.  

# Collaborer à plusieurs sur un projet

GitHub permet de travailler en équipe sur le même dépôt.

1. Sur la page GitHub de votre dépôt, cliquez sur **Settings → Collaborators**  
2. Cliquez sur **Add people**  
3. Saisissez le nom d’utilisateur GitHub de vos collègues pour le projet  
4. Il recevra une invitation par mail pour rejoindre le projet

Les collaborateurs peuvent **cloner**, **modifier**, **committer** et **pousser** leurs changements.

# Récapitulatif visuel du workflow GitHub Desktop

| Étape | Action | Description |
|-------|---------|-------------|
| 1 | **Clone** | Copier un dépôt GitHub sur votre ordinateur |
| 2 | **Edit** | Modifier les fichiers du projet |
| 3 | **Commit** | Enregistrer une nouvelle version du projet |
| 4 | **Push** | Envoyer vos changements sur GitHub |
| 5 | **Pull** | Récupérer les modifications faites par les autres |
| 6 | **Branch / Merge** | Travailler sur des fonctionnalités séparées puis fusionner |

# Conseils et bonnes pratiques

- **Commitez souvent** : un petit commit par modification logique  
- **Soyez clair** : utilisez des messages de commit descriptifs  
- **Travaillez sur des branches** : pour éviter les conflits  
- **Poussez régulièrement** : pour garder votre dépôt à jour  
- **Utilisez les issues GitHub** : pour signaler des tâches ou des bugs  

# À retenir

- Git garde l’historique des versions d’un projet  
- GitHub héberge les dépôts en ligne pour faciliter la collaboration  
- GitHub Desktop permet de tout faire sans ligne de commande  
- Les principales étapes sont : **Clone → Edit → Commit → Push → Merge**

# Liens utiles

- [Stratégie de gestion de branches](https://dev.to/juniourrau/6-types-of-git-branching-strategy-g54)
- [Initiation à GitHub Desktop](https://docs.github.com/fr/desktop/overview/)