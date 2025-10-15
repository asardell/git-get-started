Chapitre 3 : Commandes utiles


- [Objectifs](#objectifs)
- [Gestion d'une branche](#gestion-dune-branche)
  - [Commandes concernées](#commandes-concernées)
  - [Exercices](#exercices)
- [Première merge request](#première-merge-request)
  - [Depuis l'interface GitHub](#depuis-linterface-github)
  - [Mettre à jour le repos local](#mettre-à-jour-le-repos-local)
- [Travailler en collaboration](#travailler-en-collaboration)
- [Explorer l'historique](#explorer-lhistorique)
  - [`git log -n --oneline`](#git-log--n---oneline)
  - [`git log origin/main -n 10 --oneline`](#git-log-originmain--n-10---oneline)
  - [`git show <commit|tag>`](#git-show-committag)
- [Gestion de conflit lors d’un rebase](#gestion-de-conflit-lors-dun-rebase)
  - [Créer la branche `titi` :](#créer-la-branche-titi-)
  - [Créer la branche `tutu` depuis `develop` :](#créer-la-branche-tutu-depuis-develop-)
  - [Rebase de `tutu` sur `titi`](#rebase-de-tutu-sur-titi)
  - [Identifier et résoudre le conflit](#identifier-et-résoudre-le-conflit)
  - [Résoudre le conflit](#résoudre-le-conflit)
  - [Continuer le rebase](#continuer-le-rebase)
  - [Vérification](#vérification)
  - [Astuces](#astuces)
- [Explorer l'historique](#explorer-lhistorique-1)
  - [`git log -n --oneline`](#git-log--n---oneline-1)
  - [`git log origin/main -n 10 --oneline`](#git-log-originmain--n-10---oneline-1)
  - [`git show <commit|tag>`](#git-show-committag-1)
- [Liens utiles](#liens-utiles)
- [Aller plus loin](#aller-plus-loin)
- [Tableau récapitulatif des commandes Git](#tableau-récapitulatif-des-commandes-git)


## Objectifs

Voici les objectifs de ce module :
- [ ] Suivre, enregistrer et restaurer des fichiers (`add`, `commit`, `restore`, `reset`).  
- [ ] Explorer l’historique (`log`).  
- [ ] Créer, changer et supprimer des branches.  
- [ ] Travailler avec un dépôt distant (`push`, `pull`, `fetch`).  
- [ ] Résoudre des conflits et utiliser `rebase`.  
- [ ] Mettre du travail de côté et le restaurer (`stash`).  
- [ ] Réécrire l’historique (`commit --amend`, `rebase -i`).  
- [ ] Sélectionner des commits précis (`cherry-pick`).  
- [ ] Gérer des versions avec des tags (`tag`, `show`)

## Gestion d'une branche

Dans cette partie, nous allons concidérer que nous avons cette méthodologie de gestion de branche.

<p align="center">
  <img src="https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Ffbrbhaga1k2218xj77bj.png" alt="Source de l'image" width="600"/>
</p>

### Commandes concernées

`git fetch`, `git checkout`, `git add --patch`, `git push origin`, `git restore `, `git log`.

### Exercices

1. Actualiser le repos local à partir du repos distant :

```bash
git fetch origin
```

- `git fetch` : récupère les commits, branches et tags distants sans les appliquer à ta branche locale.

- `origin` : nom par défaut du repos distant

2. Créer une nouvelle branche locale depuis `origin/main` :  

```bash
git checkout -b develop origin/main
```

Le `-b` dans la commande `git checkout -b` veut dire *branch* → c’est l’option qui indique à Git de créer une nouvelle branche avant de s’y positionner.

3. Cette branche n'existe pas encore sur le repos distant, cette commane permet de la créer aussi sur le repos distant sans faire de commit :  

```bash
git push -u origin develop
```

- `git push` : Envoie les commits de la branche locale vers un dépôt distant
- `origin` : Le nom du *remote* (le dépôt distant appelé par défaut *origin*)
- `develop` :Le nom de la branche locale qu'on veut pousser
- `-u`  : Configure la liaison (tracking) entre la branche locale et la branche distante


4. Dans la branche `develop`, modifier le fichier `README.md` et ajoute du contenu avant de le commit et push. 

```bash
echo "# Recettes de Desserts" > README.md
echo "## Tiramisu" >> README.md
echo "### Ingrédients:" >> README.md
echo "- 250g de mascarpone" >> README.md
echo "- 3 œufs" >> README.md
echo "- 100g de sucre" >> README.md
echo "- 1 paquet de biscuits à la cuillère" >> README.md
echo "- 300ml de café fort" >> README.md
echo "- Cacao en poudre" >> README.md
echo "### Préparation:" >> README.md
echo "1. Séparer les blancs des jaunes d'œufs et monter les blancs en neige." >> README.md
echo "2. Mélanger les jaunes avec le sucre, puis ajouter le mascarpone." >> README.md
echo "3. Tremper les biscuits dans le café et les disposer dans un plat." >> README.md
echo "4. Ajouter la préparation avec les jaunes d'œufs, puis répéter l'opération." >> README.md
echo "5. Saupoudrer de cacao et laisser reposer au réfrigérateur pendant 4 heures." >> README.md
echo "## Brownie" >> README.md
echo "### Ingrédients:" >> README.md
echo "- 200g de chocolat noir" >> README.md
echo "- 150g de beurre" >> README.md
echo "- 200g de sucre" >> README.md
echo "- 3 œufs" >> README.md
echo "- 100g de farine" >> README.md
echo "### Préparation:" >> README.md
echo "1. Faire fondre le chocolat et le beurre." >> README.md
echo "2. Ajouter le sucre et les œufs, puis mélanger." >> README.md
echo "3. Incorporer la farine." >> README.md
echo "4. Verser dans un moule beurré et cuire à 180°C pendant 20 à 25 minutes." >> README.md
```

On peut aussi modifier un fichier directement dans le terminal avec la commande `nano`

```bash
nano README.md
```

- Ctrl + O pour enregistrer
- Entrée → pour confirmer le nom du fichier
- Ctrl + X → pour quitter nano

5. Ajouter uniquement certains modification en staging

Fais un `git add --patch` → choisis de **stager seulement une partie** des changements.  

```bash
git add --patch README.md
```

| Touche | Signification | Description / Exemple d’usage |
|:-------|:---------------|:------------------------------|
| **y** | Yes | Ajouter ce hunk au staging area (sera inclus dans le prochain commit). |
| **n** | No | Ignorer ce hunk (ne pas l’ajouter pour l’instant). |
| **q** | Quit | Quitter `git add --patch` immédiatement, sans traiter les hunks suivants. |
| **a** | All | Ajouter **tous** les hunks restants du fichier. |
| **d** | Done (ou skip remaining) | Ne pas ajouter **aucun** des hunks restants. |
| **s** | Split | Diviser le hunk en sous-parties plus petites (si possible) pour choisir plus finement les lignes à ajouter. |
| **e** | Edit | Éditer manuellement le contenu du hunk avant de le valider (ligne par ligne). |
| **?** | Help | Afficher l’aide et la signification des options disponibles. |

6. Retirer un fichier du staging.  

```bash
git restore --staged README.md
```

Enlève le fichier `README.md` du staging area, mais ne touche pas à son contenu dans le répertoire de travail.

7. Ajouter à nouveau le fichier `README.md` en staging puis utiliser la commande `restore`.  
   
```bash
git add README.md
git restore README.md
```

Récap : 

| Commande | Effet | Efface les changements ? |
|----------|-------|--------------------------|
| `git restore --staged <fichier>` | Retire du staging seulement et équivalente à `git reset HEAD` | Non |
| `git restore  <fichier>` | Réinitialise complètement (perte de modifs non commit) | Oui |


8. Ré appliquer les modifications de la question 4.

9. Ajouter en staging et commit

```bash
git add README.md
git commit -m "[TICKET-999] Modification du fichier README.md"
```

10. Modifier un commit

Mince, avant de pousser le commit nous nous sommes trompés de numéro de ticket. 
Utiliser  `git commit --amend` pour modifier le message et  `git log -n` pour vérifier les `n` derniers commit.

```bash
git commit --amend  -m "[TICKET-123] Modification du fichier README.md"
git log -1
```

:bulb: Il est aussi possible d'ajouter des nouveaux changements sur le dernier commit, pour cela il suffit d'ajouter les fichiers concernés en staging puis de renouveller l'étape `git commit --amend`

```bash
git add <votre-fichier>
git commit --amend  --no-edit
git log -1
```

- `--no-edit` : Ajoute des changements au dernier commit sans modifier son message.
  

11.  Pousser le commit actualisé sur la branche distante

Si le commit n'était pas déjà poussé : 

```bash
git push origin
```

Si le commit modifié était déjà poussé

```bash
git push --force-with-lease
```

:warning:

| Option | Effet | Risque |
|--------|-------|--------|
| `git push --force` | Force le push et remplace tout l’historique distant | Risque d’écraser les commits des autres contributeurs sur la branche|
| `git push --force-with-lease` | Force le push uniquement si personne n’a modifié la branche distante depuis le dernier `fetch` | Plus sûr : évite d’écraser le travail des autres |

## Première merge request

### Depuis l'interface GitHub

Nous allons créer la merge request via l’interface web de GitHub.

1. Dans GitHub : New Pull Request → base = main, compare = develop
2. Clique sur Create Pull Request 
3. Regarder les changements, s'il n'y a pas de conflit
4. Merger pour valider la Pull Request

### Mettre à jour le repos local

Nous venons de faire des modifications en ligne mais il faut les synchroniser avec notre repos local.

1. Vérifier depuis quand la branche n'a pas été mise à jour

```bash
# Se placer sur main locale
git checkout main

# Vérifier la branche et les commits derrière/avant le remote
git fetch origin
git status
```

2. Mettre à jour la branche locale

```bash
git pull origin main
```

- `pull` = `fetch` + `merge`

La branche locale `main` est maintenant à jour avec GitHub online.

3. Créer un tag sur la version de la branche `main`
   
```bash
git tag -a v1.0.0 -m "Release version 1.0.0"

# Vérifier le tag
git tag

# Afficher les détails du tag
git show v1.0.0

# Pousser le tag sur le dépôt distant
git push origin v1.0.0
```

- `-a` : annoté
- `-m` : message du tag


:bulb: Le tag devient visible sur GitHub


## Travailler en collaboration

Dans cette partie, nous allons concidérer que nous avons cette méthodologie de gestion de branche.

<p align="center">
  <img src="https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fmufdlg3q1xj9tbzv0geg.png" alt="Source de l'image" width="600"/>
</p>


1. Executer ces commandes pour que le repos ressemble à la méthodologie de gestion de branche ci-dessus : 

```bash
# --- S'assurer d'être à jour avec origin/develop ---
git checkout develop
git pull origin

# Branche feature/toto from origin/develop
git checkout -b feature/toto origin/develop

# Créer et pousser un fichier pour feature/toto
echo "# Fichier feature/toto" > toto.md
echo "Contenu initial pour feature/toto" >> toto.md
git add toto.md
git commit -m "Ajout du fichier toto.md sur feature/toto"
git push -u origin feature/toto

# Branche feature/tata from origin/develop
git checkout -b feature/tata origin/develop

# Créer et pousser un fichier pour feature/tata
echo "# Fichier feature/tata" > tata.md
echo "Contenu initial pour feature/tata" >> tata.md
git add tata.md
git commit -m "Ajout du fichier tata.md sur feature/tata"
git push -u origin feature/tata
```

2. Effectuer une Merge Request (MR) de `feature/toto` dans `develop`

Cette étape se fait sur **GitHub online**. Après validation, la branche `feature/toto` est fusionnée dans `develop`.


3. Effecteur un rebase de la branche `tata` à partir de  `develop` pour récupérer les changements

```bash
# Se placer sur la branche feature/tata
git checkout feature/tata

# Rebase directement depuis origin/develop
git fetch origin
git rebase origin/develop
```

4. Pousser les changements sur la branche distant (cas : sans conflit)

```bash
git push origin feature/tata #si pas de conflit
```

5. Effectuer une Merge Request (MR) de `feature/tata` dans `develop`

Cette étape se fait sur **GitHub online**. Après validation, la branche `feature/tata` est fusionnée dans `develop`.

6. Squash des 2 derniers commit de `develop` pour simplifier l'historique

```bash
git fetch origin

# Se placer sur develop
git checkout develop

# Afficher les derniers commit
git log -3

# Rebase interactif sur les 2 derniers commits
git rebase -i HEAD~2
```

- Dans l’éditeur qui s’ouvre, remplacer `pick` par `squash` pour fusionner le deuxième commit avec le premier.
- Sauvegarder et quitter pour appliquer le squash.

| Commande | Description |
|----------|-------------|
|`ECHAP` +  `:q!` | Quitte l’éditeur sans sauvegarder (dans Vim). |
|`ECHAP` + `:wq` | Quitte l’éditeur en sauvegardant (dans Vim). |

7. Pousser les changements sur la branche distante

Si tu modifies l’historique d’une branche qui **a déjà été poussée sur le repos distant**, alors Git détectera que l’historique local ne correspond plus à celui du remote.  

Dans ce cas, il faut utiliser **un push forcé** pour mettre à jour le remote avec l’historique rebased :

```bash
git push --force-with-lease
```

:bulb: Cette option vérifie que personne n’a poussé de commits sur le remote entre-temps.  

8. Effectuer une Merge Request (MR) de `develop` dans `main`

Cette étape se fait sur **GitHub online**. Après validation, la branche `develop` est fusionnée dans `main`.

1. Ajouter un tag sur la version actualisé de `main`

```bash
git fetch origin

# Se placer sur main
git checkout main
git pull origin main

# Créer un tag annoté
git tag -a V1.1.0 -m "Version 1.1.0"

# Pousser le tag sur le remote
git push origin V1.1.0
```


3.  Suppression des branche locales


```bash
# Supprimer les branches locales fusionnées
git branch -d feature/toto
git branch -d feature/tata

#ou

# Supprimer les branches supprimées sur le repos distant
git fetch -p
```

## Explorer l'historique

Dans cette section, nous allons apprendre à utiliser quelques commandes Git utiles pour **explorer l’historique des commits** et **examiner un commit ou un tag spécifique**.

---

### `git log -n --oneline`


```bash
git log -n 5 --oneline
```

- `-n 5` : limite l’affichage aux **5 derniers commits**.  
- `--oneline` : affiche chaque commit sur **une seule ligne**, avec son identifiant abrégé et le message de commit.

:bulb Très pratique pour voir rapidement les derniers commits sans tout le détail.

### `git log origin/main -n 10 --oneline`

```bash
git log origin/main -n 10 --oneline
```

- Affiche les **10 derniers commits** de la branche `main` sur le remote `origin`.  
- Permet de vérifier l’état du remote sans changer ta branche locale.

:bulb:  Utile pour comparer une branche locale avec le remote.


### `git show <commit|tag>`

```bash
git show v1.1.0
```

- Affiche les **détails d’un commit ou d’un tag** :  
- Peut être utilisé avec un **hash de commit** (id d'un commit) ou un **tag** (`v1.1.0`).

:bulb: Très pratique pour inspecter le contenu exact d’un commit ou d’un tag, surtout avant un merge.

## Gestion de conflit lors d’un rebase

Dans cette section, nous allons créer un **exemple concret** pour voir comment gérer un conflit qui apparaît lors d’un rebase.

### Créer la branche `titi` :

```bash
git fetch origin
git checkout -b feature/titi origin/develop
```

Modifier un fichier `example.txt` :

```bash
echo "Contenu de titi" > example.txt
git add example.txt
git commit -m "Modification sur feature/titi"
git push -u origin feature/titi
```

### Créer la branche `tutu` depuis `develop` :

```bash
git checkout -b feature/tutu origin/develop
```

Modifier **un fichier avec le même nom `example.txt`** :

```bash
echo "Contenu de tutu" > example.txt
git add example.txt
git commit -m "Modification sur feature/tutu"
git push -u origin feature/tutu
```

### Rebase de `tutu` sur `titi`

```bash
git fetch origin
git checkout feature/tutu
git rebase origin/feature/titi
```

:warning: Ici, Git détecte un **conflit**, car `example.txt` a été modifié dans les deux branches.

### Identifier et résoudre le conflit

Git indique les fichiers en conflit :

```bash
CONFLICT (content): Merge conflict in example.txt
```

Ouvrir le fichier `example.txt` :

````markdown
```text
<<<<<<< HEAD
Contenu de tutu
=======
Contenu de titi
>>>>>>> feature/titi
```
````

- Tout ce qui est **entre `<<<<<<< HEAD` et `=======`** correspond à ta branche actuelle (`tutu`).  
- Tout ce qui est **entre `=======` et `>>>>>>> feature/titi`** correspond à la branche sur laquelle tu rebases (`titi`).

### Résoudre le conflit

Éditer le fichier pour choisir le contenu désiré, par exemple :

```text
Contenu combiné : titi + tutu
```

Puis :

```bash
git add example.txt
```

---

### Continuer le rebase

- Git peut demander plusieurs étapes si plusieurs fichiers ont des conflits.  
- Une fois tous les conflits résolus :

```bash
git rebase --continue
git push --force-with-lease
```

### Vérification

- Afficher l’historique pour vérifier que le rebase est terminé :

```bash
git log --oneline --graph
```

- Le commit de `feature/tutu` est maintenant "rejoué" au-dessus de `feature/titi`.


### Astuces

1. **Avant un rebase**, toujours faire `git fetch origin` pour être sûr que le remote est à jour.  
2. En cas de conflit complexe, il est possible d’utiliser :

```bash
git status
```

pour voir les fichiers en conflit et `git diff` pour examiner les différences.  


3. Pour annuler un rebase en cours si ça devient trop compliqué :

```bash
git rebase --abort
```


## Explorer l'historique

Dans cette section, nous allons apprendre à utiliser quelques commandes Git utiles pour **explorer l’historique des commits** et **examiner un commit ou un tag spécifique**.

---

### `git log -n --oneline`


```bash
git log -n 5 --oneline
```

- `-n 5` : limite l’affichage aux **5 derniers commits**.  
- `--oneline` : affiche chaque commit sur **une seule ligne**, avec son identifiant abrégé et le message de commit.

:bulb Très pratique pour voir rapidement les derniers commits sans tout le détail.

### `git log origin/main -n 10 --oneline`

```bash
git log origin/main -n 10 --oneline
```

- Affiche les **10 derniers commits** de la branche `main` sur le remote `origin`.  
- Permet de vérifier l’état du remote sans changer ta branche locale.

:bulb:  Utile pour comparer une branche locale avec le remote.


### `git show <commit|tag>`

```bash
git show v1.1.0
```

- Affiche les **détails d’un commit ou d’un tag** :  
- Peut être utilisé avec un **hash de commit** (id d'un commit) ou un **tag** (`v1.1.0`).

:bulb: Très pratique pour inspecter le contenu exact d’un commit ou d’un tag, surtout avant un merge.

## Liens utiles

- [Get Started - GitHub](https://docs.github.com/fr/get-started/start-your-journey/hello-world)
- [Get started - GitHub Desktop](https://docs.github.com/fr/desktop/overview/getting-started-with-github-desktop)
- [6 Types of Git Branching](https://dev.to/juniourrau/6-types-of-git-branching-strategy-g54)

## Aller plus loin

- git graph
- git ignore

## Tableau récapitulatif des commandes Git

| Commande | Description |
|----------|-------------|
| `git add --patch` | Ajoute sélectivement des parties d’un fichier dans l’index. |
| `git commit -m "message"` | Valide les changements indexés avec un message. |
| `git push origin` | Envoie les commits locaux vers le dépôt distant. |
| `git checkout -b nom-branche origin/nom-distant` | Crée et bascule sur une nouvelle branche locale basée sur une distante. |
| `git branch -D nom-de-la-branche` | Supprime une branche locale de manière forcée. |
| `git push origin --delete nom-de-la-branche` | Supprime une branche sur le dépôt distant. |
| `git push -u origin nom-de-la-branche` | Pousse une nouvelle branche locale et définit le suivi avec le distant. |
| `git pull --rebase origin nom-de-la-branche` | Récupère les changements distants et les rejoue au-dessus des commits locaux. |
| `git stash` | Met de côté les modifications non validées. |
| `git stash pop` | Restaure les modifications précédemment stachées et supprime l’entrée du stash. |
| `git rebase -i HEAD~n` | Lance un rebase interactif sur les `n` derniers commits. |
| `git restore nom-fichier` | Restaure un fichier modifié depuis l’index ou HEAD. |
| `git restore .` | Restaure tous les fichiers modifiés. |
| `git restore --staged nom-fichier` | Retire un fichier de l’index tout en conservant les modifications. |
| `git restore --source=HEAD~1 fichier` | Restaure un fichier depuis un commit spécifique (ici le parent du HEAD). |
| `git reset HEAD nom-fichier` | Retire un fichier de l’index (équivalent à `restore --staged`). |
| `git reset --soft HEAD~n` | Déplace HEAD en arrière de `n` commits mais conserve les changements en staging. |
| `git reset --mixed HEAD~n` | Déplace HEAD en arrière et garde les changements dans le working directory. |
| `git reset --hard HEAD~n` | Déplace HEAD en arrière et supprime toutes les modifications. |
| `git log` | Affiche l’historique détaillé des commits. |
| `git log -n --oneline` | Affiche les `n` derniers commits de manière condensée. |
| `git log origin/A -n 10 --oneline` | Montre les 10 derniers commits de la branche distante `origin/A`. |
| `git push --force-with-lease` | Force le push mais en s’assurant que personne n’a écrasé les commits distants entre-temps. |
| `git fetch --all` | Récupère toutes les références du dépôt distant. |
| `git fetch --prune` | Supprime localement les références de branches distantes supprimées. |
| `git branch -r` | Liste uniquement les branches distantes. |
| `git branch -a` | Liste toutes les branches (locales et distantes). |
| `git pull --rebase origin main` | Met à jour la branche courante depuis `origin/main` avec rebase. |
| `git rebase origin/xxx/xxx` | Rebase la branche courante sur une branche distante spécifique. |
| `git rebase -i HEAD~n` | Rebase interactif sur les `n` derniers commits (squash, reword, etc.). |
| `git rebase -i origin/release/xxx-1.5.0` | Rebase interactif par rapport à une branche de release distante. |
| `git cherry-pick <hash>` | Applique un commit spécifique dans la branche courante. |
| `git cherry-pick <hash1> <hash2> ...` | Applique plusieurs commits spécifiques. |
| `git cherry-pick <hash_début>^..<hash_fin>` | Applique une plage de commits. |
| `git tag -a v1.0.0 -m "Release v1.0.0"` | Crée un tag annoté avec un message. |
| `git tag` | Liste les tags existants. |
| `git show v1.0.0` | Affiche les détails du commit associé au tag. |
| `git commit --amend -m "Nouveau message"` | Modifie le message du dernier commit. |
| `git commit --amend --no-edit` | Ajoute des changements au dernier commit sans modifier son message. |
| `git push --force-with-lease` | Met à jour l’historique distant après rebase ou amend, sans écraser les commits d’autrui. |
| `:q!` | Quitte l’éditeur sans sauvegarder (dans Vim). |
| `:wq` | Quitte l’éditeur en sauvegardant (dans Vim). |

