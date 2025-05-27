# Tutoriel Git : De débutant à avancé 🚀  

Bienvenue dans ce dépôt contenant un **tutoriel complet sur Git**, de l'initiation aux concepts avancés.  
Chaque chapitre est présenté dans un fichier `.md` distinct pour faciliter la lecture et la pratique.  

## Contenu du tutoriel  

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


### 3. Travailler avec les commit

- Ajouter tous les fichiers ou une sélection 
- Modifier un commit
- Corriger un commit déjà poussé  


### Commandes en vrac

Commande afficher comme aide-mémo le temps de rédiger un chapitre sur ces notions.

# Récapitulatif

| Commande                                 | Description                                        |
|------------------------------------------|----------------------------------------------------|
| `git rebase origin/release/tata`                    | Rebase la branche courante sur `release/tata` (branche distante)           |
| `git add -p`                                        | Ajoute les changements par blocs interactifs (patchs)                      |
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
