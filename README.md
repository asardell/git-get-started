# Tutoriel Git : De débutant à avancé 🚀  

Bienvenue dans ce dépôt contenant un **tutoriel complet sur Git**, de l'initiation aux concepts avancés.  
Chaque chapitre est présenté dans un fichier `.md` distinct pour faciliter la lecture et la pratique.  

## Contenu du tutoriel  

### 0. Git avec Github Desktop
- Créer un compte GitHub
- Créer un dépôt (repository) en ligne sur GitHub
- Gérer un projet localement avec GitHub Desktop
- Comprendre les notions de commit, branche et synchronisation
- Travailler en équipe sans ligne de commande

### 1. Introduction à Git  
- Qu'est-ce que Git ?  
- Installation et configuration  
- Premières commandes  
- Création d’un dépôt local  
- Ajout de fichiers et commits  
- États de Git (working directory, staging, repository)  
- Création et changement de branches  
- Fusion de branches  
- Suppression et bonnes pratiques  

### 2. Travailler avec un dépôt distant (GitHub/GitLab)  
- Connexion d’un dépôt local à GitHub  
- Push, Pull et Fetch  
- Vérification de la connexion  


### 3. Commandes utiles
- Suivre, enregistrer et restaurer des fichiers (`add`, `commit`, `restore`, `reset`).  
- Explorer l’historique (`log`).  
- Créer, changer et supprimer des branches.  
- Travailler avec un dépôt distant (`push`, `pull`, `fetch`).  
- Résoudre des conflits et utiliser `rebase`.  
- Mettre du travail de côté et le restaurer (`stash`).  
- Réécrire l’historique (`commit --amend`, `rebase -i`).  
- Sélectionner des commits précis (`cherry-pick`).  
- Gérer des versions avec des tags (`tag`, `show`)


### Commandes en vrac

| Commande                                 | Description                                        |
|------------------------------------------|----------------------------------------------------|
| `git rebase origin/release/tata`                    | Rebase la branche courante sur `release/tata` (branche distante)           |
| `git add --patch`                                        | Ajoute les changements par blocs interactifs (patchs)                      |
| `git rebase --continue`                             | Continue un rebase après avoir résolu les conflits                         |
| `git rebase --abort`                                | Annule complètement le rebase en cours                                     |
| `git push origin toto --force`                      | Pousse la branche `toto` en forçant le push après un rebase                |
| `git diff origin/release/tata...toto`               | Affiche les différences entre `release/tata` et `toto`                     |
| `git log origin/release/tata..toto`                 | Liste les commits présents sur `toto` mais pas sur `release/tata`         |
| `git checkout -b nom-branche origin/nom-distant`    | Crée une nouvelle branche locale à partir d’une branche distante          |
| `git branch -D nom-de-la-branche`                   | Supprime une branche locale même si non mergée                            |
| `git push origin --delete nom-de-la-branche`        | Supprime une branche sur le dépôt distant                                  |
| `git push -u origin nom-de-la-branche`              | Pousse une nouvelle branche et crée le lien de suivi avec le distant      |
| `git pull --rebase origin nom-de-la-branche`        | Récupère et rebase la branche distante sur la branche locale              |
| `git log origin/branche..HEAD --oneline`            | Compare les commits locaux vs distants                                     |
| `git stash`           | Sauvegarde temporairement les modifications non commitées   |
| `git stash pop`       | Récupère et applique le dernier stash sauvegardé            |
| `git stash list`      | Liste les éléments sauvegardés en stash      
| `git rebase -i HEAD~3`          | Rebase interactif sur les 3 derniers commits       |
| `git rebase -i HEAD~n`          | Rebase interactif sur les `n` derniers commits     |
| `:q!`        | Quitter sans sauvegarder           |
| `:wq`        | Sauvegarder et quitter             |
| `git restore nom-fichier`           | Annule les modifications locales d’un fichier (non commitées)              |
| `git restore .`                     | Annule toutes les modifications non commitées dans le répertoire courant   |
| `git restore --staged nom-fichier`  | Retire un fichier de l’index (zone de staging) sans supprimer les modifs   |
| `git restore --source=HEAD~1 fichier` | Remplace un fichier avec sa version du commit précédent (`HEAD~1`)         |
| `git reset HEAD nom-fichier`              | Retire le fichier de l'index (unstage) sans perdre les modifications        |
| `git reset --soft HEAD~1`                 | Annule le dernier commit, conserve les fichiers dans l'index et le working dir |
| `git reset --mixed HEAD~1`                | Annule le dernier commit, conserve les fichiers modifiés (par défaut)       |
| `git reset --hard HEAD~1`                 | Supprime le dernier commit **et** les modifications locales (**danger**)    |
| `git log`                                             | Affiche l’historique des commits pour récupérer les hashes                                       |
| `git log -3 --oneline`                                | Affiche les 3 derniers commits en résumé                                                          |
| `git log -n 5 --oneline`                              | Affiche les 5 derniers commits en résumé                                                          |
| `git reset --soft HEAD~2`                             | Annule les 2 derniers commits en gardant les fichiers et l’index (zone de staging)                |
| `git reset --hard HEAD~2`                             | Supprime les 2 derniers commits et toutes les modifications locales (**danger**)                  |
| `git reset --hard HEAD~1`                             | Supprime le dernier commit et les changements locaux (**danger**)                                 |
| `git revert <hash>`                                   | Crée un commit qui annule le commit spécifié sans réécrire l’historique                           |
| `git push origin <nom-de-ta-branche> --force`         | Force le push de ta branche locale (utile après un reset ou rebase)                               |
| `git push --force-with-lease`                         | Force le push mais vérifie qu’il n’y a pas eu d’autres changements distants                       |
| `git stash`                                           | Met de côté les modifications non commitées (working directory propre)                            |
| `git stash list`                                      | Liste les changements mis de côté                                                                 |
| `git stash pop`                                       | Récupère et applique les derniers changements mis en stash                                        |
| `git restore <file_name>`                             | Annule les modifications locales sur un fichier (working directory)                               |
| `git fetch --all`                                     | Récupère toutes les branches distantes                                                            |
| `git fetch --prune`                                   | Supprime les références locales des branches distantes supprimées                                 |
| `git branch -r`                                       | Liste toutes les branches distantes                                                               |
| `git pull --rebase origin main`                       | Rebase ta branche locale sur la dernière version de `main` (historique plus propre)               |
| `git rebase origin/release`                           | Rebase ta branche locale sur `origin/release`                                                     |
| `git rebase origin/xxx/xxx`                           | Rebase ta branche locale sur une branche distante spécifique                                      |
| `git rebase -i HEAD~n`                                | Rebase interactif sur les `n` derniers commits pour squasher ou modifier les messages              |
| `git rebase -i origin/release/xxx-1.5.0`              | Rebase interactif à partir d’une branche distante pour faire du squash                             |
| `git cherry-pick <hash>`                              | Applique un commit précis d’une autre branche sur ta branche courante                              |
| `:q!`                                                 | Quitter l’éditeur sans sauvegarder                                                                 |
| `:wq`                                                 | Sauvegarder et quitter l’éditeur                      
| `git restore --staged <fichier>`                               | Retire le fichier de la zone de staging, conserve les modifications locales |
| `git restore --staged <fichier>` + `git restore <fichier>`     | Retire le fichier du staging **et** annule les modifications locales         |
| `git log origin/A -n 10 --oneline` | Affiche les 10 derniers commits de la branche distante `origin/A` en format compact |
| `git cherry-pick <hash1> <hash2> ... <hash10>` | Applique plusieurs commits spécifiques (listés par leurs hash) sur la branche courante |
| `git cherry-pick <hash_début>^..<hash_fin>` | Applique une plage de commits (du commit de début au commit de fin inclus) |
| `git push origin B` | Pousse la branche locale sur la branche `B` du dépôt distant |
| `git reset --hard HEAD~10` | Supprime les 10 derniers commits de ta branche locale (⚠ irréversible si non sauvegardé ailleurs) |
| `git push origin --force-with-lease` | Force la mise à jour de la branche distante tout en vérifiant qu’elle n’a pas changé entre-temps |
| `git branch -a` | Liste toutes les branches locales **et** distantes |
| `git branch -r` | Liste uniquement les branches distantes |
| `git tag -a v1.0.0 -m "Release v1.0.0"` | Crée un tag annoté `v1.0.0` avec un message |
| `git tag` | Liste tous les tags du dépôt |
| `git show v1.0.0` | Affiche les détails du commit correspondant au tag `v1.0.0` |
| `git commit --amend -m "Nouveau message"` | Modifie le message du **dernier commit** |
| `git commit --amend --no-edit` | Met à jour le contenu du dernier commit sans modifier son message |
| `git push --force-with-lease` | Met à jour la branche distante avec la version corrigée (après un amend) |

## Liens utiles

- [Stratégie de gestion de branches](https://dev.to/juniourrau/6-types-of-git-branching-strategy-g54)
- [Markdown Cheat Sheet](https://www.markdownguide.org/cheat-sheet/)
- [GitHub Cheat Sheet](https://training.github.com/downloads/fr/github-git-cheat-sheet.pdf)
- [GitHub Get Started](https://docs.github.com/fr/get-started/quickstart/hello-world)
- [GitHub Set up](https://docs.github.com/fr/get-started/quickstart/set-up-git)
- [Initiation à GitHub Desktop](https://docs.github.com/fr/desktop/overview/)