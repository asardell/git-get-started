Les bases de git

Voici les objectifs de ce cours  :
- [ ] Installer git
- [ ] Initialiser son premier dépôt git
- [ ] Travailler avec des branches
- [ ] Se familiariser avec les commandes de base

1. [Introduction à Git et installation](#introduction-à-git-et-installation)
   1. [Qu'est-ce que Git et comment fonctionne-t-il ?](#quest-ce-que-git-et-comment-fonctionne-t-il-)
      1. [Les 3 zones principales de Git](#les-3-zones-principales-de-git)
      2. [🔄 Résumé du workflow Git](#-résumé-du-workflow-git)
   2. [Vérifier la version de Git](#vérifier-la-version-de-git)
   3. [Configurer son identité Git](#configurer-son-identité-git)
   4. [Vérifier la configuration Git](#vérifier-la-configuration-git)
2. [Initialisation et gestion d'un dépôt](#initialisation-et-gestion-dun-dépôt)
   1. [Initialiser un dépôt Git](#initialiser-un-dépôt-git)
   2. [Ajouter un fichier README.md](#ajouter-un-fichier-readmemd)
   3. [Ajouter un fichier au suivi Git](#ajouter-un-fichier-au-suivi-git)
   4. [Sauvegarder les modifications avec un commit](#sauvegarder-les-modifications-avec-un-commit)
   5. [Vérifier l'état du dépôt](#vérifier-létat-du-dépôt)
3. [Travailler avec des branches](#travailler-avec-des-branches)
   1. [Vérifier les branches disponibles](#vérifier-les-branches-disponibles)
   2. [Créer et basculer sur une nouvelle branche](#créer-et-basculer-sur-une-nouvelle-branche)
   3. [Modifier le fichier README.md](#modifier-le-fichier-readmemd)
   4. [Vérifier les modifications](#vérifier-les-modifications)
   5. [Ajouter les modifications au suivi Git](#ajouter-les-modifications-au-suivi-git)
   6. [Créer un commit pour sauvegarder la modification](#créer-un-commit-pour-sauvegarder-la-modification)
   7. [Revenir sur la branche principale](#revenir-sur-la-branche-principale)
   8. [Fusionner la branche dans main](#fusionner-la-branche-dans-main)
   9. [Supprimer la branche après fusion](#supprimer-la-branche-après-fusion)
4. [Récapitulatif](#récapitulatif)

 
# Introduction à Git et installation

## Qu'est-ce que Git et comment fonctionne-t-il ?

Git est un **système de gestion de versions** utilisé par les développeurs pour suivre les modifications du code, collaborer et gérer différentes versions d'un projet.

### Les 3 zones principales de Git  

![](./img/git%20zone.png)

1. **Working Directory (Dossier de travail)**  
   - C'est l'endroit où tu modifies et crées des fichiers.  
   - Les changements ici **ne sont pas encore suivis** par Git.  

2. **Staging Area (Index)**  
   - Lorsque tu fais `git add`, les fichiers sont ajoutés à cette zone intermédiaire.  
   - Cela permet de **préparer les fichiers** avant de les valider définitivement.  

3. **Repository Distant (Remote)**  
   - C'est le serveur où le code est stocké et partagé avec l'équipe (ex: GitHub, GitLab).  
   - `git push` envoie les commits locaux au repo distant, et `git pull` récupère les mises à jour.  

### 🔄 Résumé du workflow Git  

```plaintext
📂 Working Directory → (git add) → 📝 Staging Area → (git commit) → 📦 Local Repository → (git push) → 🌍 Remote Repository
```

## Vérifier la version de Git
Avant de commencer, assurez-vous que Git est bien installé en vérifiant sa version.

```bash
git --version
```

Explication des éléments :

- `git` : Exécute la commande Git.
- `--version` : Affiche la version actuelle de Git installée sur votre machine.

## Configurer son identité Git
Git utilise votre nom et votre email pour associer chaque commit à son auteur.

```bash
git config --global user.name "Votre Nom"
git config --global user.email "votre.email@example.com"
```

Explication des éléments :
- `git config` : Configure les paramètres Git.
- `--global` : Applique la configuration à tous les dépôts de l'utilisateur.
- `user.name` : Définit votre nom d’utilisateur Git.
- `user.email` : Définit votre adresse email associée aux commits.

## Vérifier la configuration Git
Pour s'assurer que les configurations ont bien été enregistrées, on peut afficher la liste des paramètres configurés.

```bash
git config --list
```

Explication des éléments :
- `git config` : Accède aux configurations Git.
- `--list` : Affiche toutes les configurations actuelles.


# Initialisation et gestion d'un dépôt
Avant d’utiliser Git, nous devons créer un dossier pour notre projet.

```bash
mkdir mon-projet
cd mon-projet
```
Explication des éléments :
- `mkdir mon-projet` : Crée un dossier nommé mon-projet.
- `cd mon-projet` : Entre dans ce dossier pour y travailler.
- `cd` : commande *change directory*.

## Initialiser un dépôt Git
Un dépôt Git doit être initialisé avant d’être utilisé pour le versionnement.

```bash
git init
```

Explication des éléments :
- `git init` : Initialise un dépôt Git dans le dossier courant.
Cela crée un dossier .git qui stocke l’historique et les configurations du dépôt.

## Ajouter un fichier README.md
Un fichier README.md permet de documenter un projet.

```bash
echo "# Mon Projet" > README.md
```
Explication des éléments :
- `echo "# Mon Projet"` : Crée une ligne de texte avec # Mon Projet.
- `>` : Redirige la sortie vers un fichier (écrase s’il existe déjà).
- `README.md` : Nom du fichier dans lequel écrire.


## Ajouter un fichier au suivi Git
Nous devons informer Git des fichiers à suivre.

```bash
git add README.md
```
Explication des éléments :
- `git add` : Ajoute des fichiers à la zone de staging.
- `README.md` : Spécifie le fichier à ajouter.

## Sauvegarder les modifications avec un commit
Un commit permet d’enregistrer les changements dans l’historique Git.

```bash
git commit -m "Initial commit: Add README.md"
```
Explication des éléments :
- `git commit` : Crée un instantané des fichiers suivis.
- `-m` : Ajoute un message de description.

## Vérifier l'état du dépôt
On peut voir les fichiers modifiés ou en attente de commit.

```bash
git status
```
Explication des éléments :
- `git status` : Affiche l’état des fichiers suivis et non suivis par Git.

# Travailler avec des branches

## Vérifier les branches disponibles
Les branches permettent de travailler sur des fonctionnalités indépendamment.

```bash
git branch
```
Explication des éléments :
- `git branch` : Liste les branches disponibles dans le dépôt local.

## Créer et basculer sur une nouvelle branche
On crée une nouvelle branche pour travailler sur une fonctionnalité spécifique.

```bash
git checkout -b feature/login
```
Explication des éléments :
- `git checkout -b` : Crée une nouvelle branche et s’y positionne directement.
- `feature/login` : Nom de la nouvelle branche.


## Modifier le fichier README.md
On ajoute une nouvelle ligne dans notre fichier README.md.

```bash
echo "Ajout d'une description du projet." >> README.md
```
Explication des éléments :
- `echo "Texte"` : Ajoute du texte.
- `>>` : Ajoute à la fin du fichier sans écraser son contenu.
- `README.md` : Fichier cible de la modification.


## Vérifier les modifications
On peut voir si des fichiers ont été modifiés depuis le dernier commit.

```bash
git status
```
On peut aussi voir les modifications exactes effectuées dans un fichier.

```bash
git diff README.md
```
Explication des éléments :
- `git diff` : Compare les modifications non encore validées.
- `README.md` : Spécifie le fichier à comparer.

## Ajouter les modifications au suivi Git
On enregistre la modification de README.md dans la zone de staging.

```bash
git add README.md
```

## Créer un commit pour sauvegarder la modification
On valide la modification avec un message explicatif.

```bash
git commit -m "Update README.md"
```
Explication des éléments :
- `git commit` : Enregistre les modifications suivies.
- `-m "Message"` : Définit un message de commit décrivant la modification.

## Revenir sur la branche principale
Avant d’intégrer notre branche, nous devons revenir sur main.

```bash
git checkout main
```
Explication des éléments :
- `git checkout` : Change de branche.
- `main` : Spécifie la branche à rejoindre.


## Fusionner la branche dans main
On intègre les modifications de feature/login dans main.

```bash
git merge feature/login -m "Merge feature/login into main"
```
Explication des éléments :
- `git merge` : Fusionne la branche spécifiée dans la branche courante.
- `feature/login` : Nom de la branche à fusionner.
- `-m "Merge feature/login into main"` : Ajoute un message de commit de fusion.


## Supprimer la branche après fusion
Une fois fusionnée, la branche feature/login n’est plus nécessaire.

```bash
git branch -d feature/login
```
Explication des éléments :
- `git branch -d` : Supprime une branche locale si elle est fusionnée.
- `feature/login` : Nom de la branche à supprimer.


# Récapitulatif

| Commande                                 | Description                          |
|------------------------------------------|--------------------------------------|
| `git --version`                                                       | Vérifie la version actuelle de Git installée sur la machine.                                   |
| `git config --global user.name "Votre Nom"`                            | Configure le nom d’utilisateur global pour tous les dépôts Git.                               |
| `git config --global user.email "votre.email@example.com"`             | Configure l’adresse e-mail globale pour tous les dépôts Git.                                  |
| `git config --list`                                                   | Affiche la liste complète des configurations actuelles de Git.                                |
| `mkdir mon-projet`                                                     | Crée un dossier nommé "mon-projet".                                                            |
| `cd mon-projet`                                                       | Se déplace dans le dossier "mon-projet".                                                      |
| `git init`                                                            | Initialise un nouveau dépôt Git dans le dossier courant.                                      |
| `echo "# Mon Projet" > README.md`                                      | Crée un fichier README.md et y écrit "# Mon Projet".                                           |
| `git add README.md`                                                   | Ajoute README.md à la zone de staging.                                                        |
| `git commit -m "Initial commit: Add README.md"`                        | Enregistre les modifications avec un message de commit.                                       |
| `git status`                                                          | Affiche l’état actuel des fichiers suivis et non suivis par Git.                              |
| `git branch`                                                          | Liste toutes les branches du dépôt.                                                           |
| `git checkout -b feature/login`                                        | Crée une nouvelle branche "feature/login" et bascule dessus.                                   |
| `echo "Ajout d'une description du projet." >> README.md`               | Ajoute du texte à la fin du fichier README.md.                                                 |
| `git status`                                                          | Vérifie les modifications en attente dans le dépôt.                                            |
| `git diff README.md`                                                  | Affiche les différences entre la version en cours et la dernière commitée.                   |
| `git add README.md`                                                   | Ajoute les modifications du fichier README.md à la zone de staging.                          |
| `git commit -m "Update README.md"`                                     | Enregistre les modifications du fichier avec un message de commit.                           |
| `git checkout main`                                                   | Bascule sur la branche "main".                                                                |
| `git merge feature/login -m "Merge feature/login into main"`           | Fusionne la branche "feature/login" dans "main".                                              |
| `git branch -d feature/login`                                          | Supprime la branche "feature/login" après fusion.                                             |
