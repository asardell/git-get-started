# TP : Découverte de Git - Questions & Réponses

Objectif :
- explorer les branches
- résoudre des conflits
- manipuler l’historique à l’aide des commandes de base et avancées.

1. [TP : Découverte de Git - Questions \& Réponses](#tp--découverte-de-git---questions--réponses)
   1. [Initialisation d’un dépôt](#initialisation-dun-dépôt)
   2. [Ajout de fichiers et création d’une branche à exécuter :](#ajout-de-fichiers-et-création-dune-branche-à-exécuter-)
   3. [Fusion d’une branche dans main](#fusion-dune-branche-dans-main)
   4. [Gestion des conflits](#gestion-des-conflits)
   5. [Exploration de l’historique](#exploration-de-lhistorique)
   6. [Rebase d’une branche](#rebase-dune-branche)
   7. [Cherry-pick d’un commit](#cherry-pick-dun-commit)
   8. [Gestion avancée avec git stash](#gestion-avancée-avec-git-stash)

## Initialisation d’un dépôt


```bash

mkdir git-example && cd git-example
git init
echo "# Git Example Project" > README.md
git add README.md
git commit -m "Initial commit: Add README.md"
```

Questions :

Que fait la  `git init` ?

git init initialise un dépôt Git vide dans le répertoire courant.

Quelle est la différence entre git add et git commit ?

git add place les modifications dans la zone de staging.
git commit enregistre ces modifications dans l’historique du dépôt.
Comment afficher l’historique des commits ?

Avec la  `git log`.

## Ajout de fichiers et création d’une branche à exécuter :

```bash

echo "Welcome to the project!" > index.html
git add index.html
git commit -m "Add index.html with welcome message"
git checkout -b feature/login
echo "Login Page" > login.html
git add login.html
git commit -m "Add login.html file for login page"
```
Questions :

Que fait la  `git checkout -b feature/login` ?

Elle crée une nouvelle branche appelée feature/login et bascule dessus.

Comment voir sur quelle branche vous travaillez actuellement ?

Avec la  `git branch`. L’astérisque `*` indique la branche active.

Pourquoi utiliser des branches dans un projet ?

Pour travailler sur des fonctionnalités ou des correctifs sans affecter la branche principale.

## Fusion d’une branche dans main


```bash

git checkout main
git merge feature/login -m "Merge feature/login into main"
```
Questions :

Que fait la  `git merge` ?

Elle fusionne une branche donnée dans la branche active.

Que signifie l’option `-m` dans `git merge` ?

Elle permet de spécifier un message pour le commit de fusion.

Comment Git gère-t-il automatiquement une fusion ?

Git fusionne automatiquement les branches si aucun conflit n’existe.

## Gestion des conflits


```bash

git checkout -b feature/dashboard
echo "Dashboard Page" > dashboard.html
git add dashboard.html
git commit -m "Add dashboard.html file"
echo "<h1>Dashboard Content</h1>" >> index.html
git add index.html
git commit -m "Add dashboard content to index.html"

git checkout main
echo "<footer>Footer content</footer>" >> index.html
git add index.html
git commit -m "Add footer content to index.html"

git merge feature/dashboard
```
Questions :

Pourquoi un conflit survient-il ?

Un conflit survient lorsque les mêmes lignes d’un fichier sont modifiées sur deux branches différentes.

Comment résoudre un conflit dans un fichier ?

Ouvrir le fichier concerné, analyser les balises `<<<<<<`, `=======,` et `>>>>>>,` et choisir quelles modifications garder. Ensuite, faire :

```bash

git add index.html
git commit -m "Resolve merge conflict"
```
Quelle  permet d’abandonner une fusion en cours ?

`git merge --abort`.

## Exploration de l’historique


```bash

git log --oneline --graph --all
```
Questions :

Que fait git log --oneline --graph --all ?

--oneline : Affiche les commits sous une forme abrégée.
--graph : Montre un graphe visuel des branches.
--all : Affiche toutes les branches, même celles qui ne sont pas actives.
Comment identifier un commit spécifique ?

Avec son SHA (identifiant unique) affiché par git log.

## Rebase d’une branche


```bash

git checkout feature/login
git rebase main
```
Questions :

Que fait la commande `git rebase` ?

Elle repositionne les commits de la branche courante sur la branche cible pour créer un historique linéaire.

Quelle est la différence entre merge et rebase ?

merge conserve l’historique des branches et crée un commit de fusion.
rebase réécrit l’historique pour rendre le graphe linéaire.
Que faire si un conflit survient pendant un rebase ?

Résoudre le conflit, puis utiliser :

```bash

git rebase --continue
```
Si vous voulez abandonner le rebase :

```bash
git rebase --abort
```

## Cherry-pick d’un commit


```bash
git checkout main
git cherry-pick <sha-du-commit>
```
Questions :

Que fait git cherry-pick ?

Elle copie un commit spécifique d’une branche pour l’appliquer sur la branche courante.

Quand utiliser cherry-pick ?

Quand vous voulez appliquer une modification spécifique d’une branche sans fusionner l’ensemble de la branche.

## Gestion avancée avec git stash


```bash
git checkout feature/login
echo "<div>Work in progress</div>" >> login.html
git stash
git stash list
git stash apply
git stash drop
```
Questions :

Que fait git stash ?

Elle sauvegarde temporairement les modifications non indexées pour pouvoir basculer sur une autre branche.

Quelle est la différence entre git stash apply et git stash pop ?

apply applique les modifications sans supprimer le stash.
pop applique les modifications et supprime le stash.
Comment afficher les stashes disponibles ?

Avec la commande `git stash list`.
