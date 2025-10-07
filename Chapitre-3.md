Chapitre 3 : Commandes utiles


- [Objectifs](#objectifs)
- [Gestion d'une branche](#gestion-dune-branche)
  - [Commandes concernées](#commandes-concernées)
  - [Exercices](#exercices)
- [Travailler en collaboration](#travailler-en-collaboration)
  - [Commandes concernées](#commandes-concernées-1)
  - [Exercices](#exercices-1)
- [Stash (mettre de côté du travail temporairement)](#stash-mettre-de-côté-du-travail-temporairement)
  - [Commandes concernées](#commandes-concernées-2)
  - [Exercices](#exercices-2)
- [Historique et logs](#historique-et-logs)
  - [Commandes concernées](#commandes-concernées-3)
  - [Exercices](#exercices-3)
- [Reset et restauration de versions](#reset-et-restauration-de-versions)
  - [Commandes concernées](#commandes-concernées-4)
  - [Exercices](#exercices-4)
- [Rebase et fusion de commits](#rebase-et-fusion-de-commits)
  - [Commandes concernées](#commandes-concernées-5)
  - [Exercices](#exercices-5)
- [Cherry-pick](#cherry-pick)
  - [Commandes concernées](#commandes-concernées-6)
  - [Exercices](#exercices-6)
- [Tags](#tags)
  - [Commandes concernées](#commandes-concernées-7)
  - [Exercices](#exercices-7)
- [Amend et push forcé](#amend-et-push-forcé)
  - [Commandes concernées](#commandes-concernées-8)
  - [Exercices](#exercices-8)
- [Fetch et nettoyage](#fetch-et-nettoyage)
  - [Commandes concernées](#commandes-concernées-9)
  - [Exercices](#exercices-9)
- [Liens utiles](#liens-utiles)
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
git fetch --all
```

- `git fetch` : récupère les commits, branches et tags distants sans les appliquer à ta branche locale.

- `--all` : applique cette opération à toutes les branches.

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


## Travailler en collaboration

Dans cette partie, nous allons concidérer que nous avons cette méthodologie de gestion de branche.

<p align="center">
  <img src="https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fmufdlg3q1xj9tbzv0geg.png" alt="Source de l'image" width="600"/>
</p>



### Commandes concernées
`git checkout -b nom-branche origin/nom-distant`,  
`git branch -D nom-de-la-branche`, `git push origin --delete nom-de-la-branche`,  
`git push -u origin nom-de-la-branche`, `git branch -r`, `git branch -a`

### Exercices


3. Liste les branches locales, distantes et toutes :  
   `git branch`  
   `git branch -r`  
   `git branch -a`  

4. Supprime la branche localement et sur le distant :  
   `git branch -D feature/test`  
   `git push origin --delete feature/test`



## Stash (mettre de côté du travail temporairement)

### Commandes concernées
`git stash`, `git stash pop`

### Exercices
1. Modifie un fichier **sans le committer**.  
2. Lance `git stash` → les changements disparaissent.  
3. Vérifie l’état avec `git status`.  
4. Restaure avec `git stash pop`.



## Historique et logs

### Commandes concernées
`git log`, `git log -n --oneline`,  
`git log origin/main -n 10 --oneline`, `git show v1.0.0`

### Exercices
1. Explore l’historique avec `git log` et navigue avec ↑ / ↓.  
2. Résume les 5 derniers commits :  
   `git log -5 --oneline`  
3. Compare l’historique local et distant :  
   `git log origin/main -n 10 --oneline`



## Reset et restauration de versions

### Commandes concernées
`git reset --soft HEAD~n`, `git reset --mixed HEAD~n`,  
`git reset --hard HEAD~n`, `git restore --source=HEAD~1 fichier`

### Exercices
1. Ajoute plusieurs commits rapides (`touch f1.txt`, `f2.txt`, etc.).  
2. Teste les resets :  
   - `git reset --soft HEAD~1` : les commits disparaissent mais les modifs restent **staged**.  
   - `git reset --mixed HEAD~1` : les modifs restent **dans le working directory**.  
   - `git reset --hard HEAD~1` : ⚠️ tout est supprimé.  

3. Teste `git restore --source=HEAD~1 f1.txt` pour restaurer un fichier d’une version précédente.



## Rebase et fusion de commits

### Commandes concernées
`git pull --rebase origin nom-branche`,  
`git rebase -i HEAD~n`,  
`git rebase origin/xxx/xxx`,  
`git rebase -i origin/release/xxx-1.5.0`

### Exercices
1. Mets-toi sur une branche de test et fais quelques commits.  
2. Lance `git rebase -i HEAD~3`  
   - Combine (`squash`) deux commits en un seul.  
   - Change le message d’un commit.  

3. Mets ta branche à jour avec le remote :  
   `git pull --rebase origin main`



## Cherry-pick

### Commandes concernées
`git cherry-pick <hash>`,  
`git cherry-pick <hash1> <hash2>`,  
`git cherry-pick <hash_début>^..<hash_fin>`

### Exercices
1. Identifie un commit intéressant dans `git log`.  
2. Récupère-le sur ta branche courante avec `git cherry-pick <hash>`.  
3. Teste la sélection multiple avec `git cherry-pick <hash1> <hash2>`.  
4. Teste une plage de commits avec `git cherry-pick <hash_début>^..<hash_fin>`.



## Tags

### Commandes concernées
`git tag -a v1.0.0 -m "Release v1.0.0"`, `git tag`,  
`git show v1.0.0`

### Exercices
1. Crée un tag annoté `git tag -a v1.0.0 -m "Release v1.0.0"`.  
2. Liste tous les tags avec `git tag`.  
3. Inspecte le contenu avec `git show v1.0.0`.



## Amend et push forcé

### Commandes concernées
`git push --force-with-lease`

### Exercices
1. Fais un commit avec un mauvais message.  
2. Corrige-le avec `git commit --amend -m "Meilleur message"`.  
3. Ajoute un oubli dans le commit précédent et utilise `git commit --amend --no-edit`.  
4. Envoie les changements avec `git push --force-with-lease`.


## Fetch et nettoyage

### Commandes concernées
`git fetch --all`, `git fetch --prune`

### Exercices
1. Lance `git fetch --all` pour mettre à jour toutes les branches distantes.  
2. Supprime une branche distante depuis GitHub, puis lance `git fetch --prune`.  
   → Vérifie qu’elle disparaît de la liste des branches distantes (`git branch -r`).


## Liens utiles

- [Get Started - GitHub](https://docs.github.com/fr/get-started/start-your-journey/hello-world)
- [Get started - GitHub Desktop](https://docs.github.com/fr/desktop/overview/getting-started-with-github-desktop)
- [6 Types of Git Branching](https://dev.to/juniourrau/6-types-of-git-branching-strategy-g54)

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

