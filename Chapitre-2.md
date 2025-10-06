Chapitre 2 : Travailler avec GitHub

Voici les objectifs de ce cours  :
- [ ] Associer un dépôt local à un dépôt distant
- [ ] Se connecter à un dépôt distant
- [ ] Intéragir avec le dépôt distant
 
- [Créer un dépôt local](#créer-un-dépôt-local)
  - [Créer un dépôt local pour le projet](#créer-un-dépôt-local-pour-le-projet)
  - [Configurer l'utilisateur local](#configurer-lutilisateur-local)
  - [Créer un fichier README.md](#créer-un-fichier-readmemd)
- [Connexion avec son compte GitHub](#connexion-avec-son-compte-github)
  - [Générer une clé SSH](#générer-une-clé-ssh)
  - [Nommer le fichier qui stockera les clés](#nommer-le-fichier-qui-stockera-les-clés)
  - [Définir un mot de passe pour protéger la clé privée](#définir-un-mot-de-passe-pour-protéger-la-clé-privée)
  - [Lancer l'agent SSH](#lancer-lagent-ssh)
  - [Ajouter une clé SSH à l'agent](#ajouter-une-clé-ssh-à-lagent)
  - [Afficher la clé publique SSH](#afficher-la-clé-publique-ssh)
  - [Ajouter la clé SSH](#ajouter-la-clé-ssh)
  - [Tester la connexion SSH avec GitHub](#tester-la-connexion-ssh-avec-github)
- [Collaborer avec son dépôt distant](#collaborer-avec-son-dépôt-distant)
  - [Créer un dépôt distant](#créer-un-dépôt-distant)
  - [Ajouter une origine distante](#ajouter-une-origine-distante)
  - [Pousser les modifications vers GitHub](#pousser-les-modifications-vers-github)
  - [Renommer la branche en "main"](#renommer-la-branche-en-main)
  - [Pousser les modifications vers GitHub (encore)](#pousser-les-modifications-vers-github-encore)
  - [Vérifiez votre dépôt sur GitHub](#vérifiez-votre-dépôt-sur-github)
  - [Afficher les remotes](#afficher-les-remotes)
  - [Afficher les informations sur l'origine distante](#afficher-les-informations-sur-lorigine-distante)
- [Récapitulatif](#récapitulatif)


# Créer un dépôt local

## Créer un dépôt local pour le projet
Un dossier de projet est nécessaire pour initialiser un dépôt Git.

```bash
mkdir mon-projet
cd mon-projet
git init
```
Explication des éléments :- mkdir : Commande qui crée un répertoire.
- `mon-projet` : Nom du répertoire que l'on souhaite créer.
- `cd` : Change le répertoire de travail vers celui spécifié.
- `git init` : Crée un nouveau dépôt Git dans le répertoire courant.


## Configurer l'utilisateur local
Il est important de spécifier le nom et l'email associés aux commits dans Git, et ce localement dans un projet.

```bash
git config --local user.name "VotreNom"
git config --local user.email "VotreEmail"
```
Explication des éléments :- git config : Modifie la configuration Git.
- `--local` : Applique cette configuration uniquement au dépôt courant.

## Créer un fichier README.md
Le fichier README.md sert à fournir des informations importantes sur le projet. Ici, on y ajoute un titre.

```bash
echo "# Mon Projet" > README.md
git add README.md
git commit -m "Initial commit: Add README.md"
```
Explication des éléments :
- `echo` : Affiche ou écrit une chaîne de caractères.
- `>` : Redirige la sortie vers un fichier, créant ou écrasant ce dernier.
- `README.md` : Le fichier cible dans lequel on insère le texte.
- `git add` : Ajoute des fichiers à la zone de staging.
- `git commit` : Enregistre les modifications dans l'historique de Git.
- `-m` : Permet d’ajouter un message de commit.

# Connexion avec son compte GitHub

## Ou créer la clé SSH

![](img/warning.gif)

Il est recommandé de créer la clé SSH en dehors du repository git car elle peut servir pour plusieurs projet dans le même compte utilisateur github. 

Utilisez cette commande pour vous recentrer sur le dossier parent : 

```bash
cd ..
```

## Générer une clé SSH
Cette commande génère une clé SSH pour sécuriser les connexions avec les serveurs Git.

```bash
ssh-keygen -t rsa -b 4096 -C "votre.email@example.com"
```
Explication des éléments :
- `ssh-keygen` : Génère une paire de clés SSH.
- `-t rsa` : Spécifie le type d'algorithme (RSA ici).
- `-b 4096` : Définit la longueur de la clé à 4096 bits.
- `-C` : Ajoute un commentaire, ici l'email, pour identifier la clé.

## Nommer le fichier qui stockera les clés
Lors de la génération de la clé SSH, on vous demande comment nommer le fichier contenant la clé privée et la clé publique.

```bash
Enter file in which to save the key (/c/Users/xxx/.ssh/id_rsa): toto
```

Ici, vous avez choisi *toto* comme nom de fichier.
Cela crée deux fichiers :

`toto ` : La clé privée (NE JAMAIS PARTAGER !)
`toto.pub` : La clé publique (à partager sur GitHub ou d'autres serveurs pour s'authentifier)
Par défaut, si vous ne spécifiez pas de nom, les clés sont enregistrées dans `votre_chemin/id_rsa` (clé privée) et `votre_chemin/id_rsa.pub` (clé publique).

## Définir un mot de passe pour protéger la clé privée
Après avoir choisi un nom de fichier, le terminal vous demande de saisir un passphrase (mot de passe) :

```bash
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
```

Pourquoi mettre un mot de passe ?

Cela ajoute une couche de sécurité supplémentaire : même si quelqu'un récupère votre clé privée, il devra connaître le mot de passe pour l'utiliser.
Si vous laissez le champ vide, la clé sera utilisable sans saisie de mot de passe.

Où est-elle enregistrée ?
Si vous ne précisez que le nom du fichier, la clé sera créée dans le dossier en cours dans la session Bash. 
C'est ce qu'on appelle le répertoire actif (ou Active Directory dans Git Bash).

Pour voir dans quel dossier vous êtes :

```bash
pwd
```

## Lancer l'agent SSH
L'agent SSH gère les clés SSH pour faciliter les connexions sécurisées. L'agent SSH permet de mémoriser en mémoire la clé privée et d'éviter de retaper le mot de passe à chaque utilisation.

```bash
eval "$(ssh-agent -s)"
```
Explication des éléments :
- `eval` : Exécute la commande dans le shell actuel.
- `$(ssh-agent -s)` : Lance l'agent SSH en arrière-plan et récupère son identifiant.

## Ajouter une clé SSH à l'agent
Cette commande ajoute la clé SSH générée à l'agent pour une utilisation automatique.

```bash
ssh-add votre_chemin/toto
```
Explication des éléments :
- `ssh-add` : Ajoute une clé privée SSH à l'agent.
- `votre_chemin/toto` : Chemin du fichier contenant la clé privée à ajouter.

## Afficher la clé publique SSH
Cela permet de récupérer la clé publique générée afin de l'ajouter à des services comme GitHub.

```bash
cat votre_chemin/toto.pub
```
Explication des éléments :
- `cat` : Affiche le contenu d'un fichier.
- `votre_chemin/toto.pub` : Chemin du fichier de la clé publique.

## Ajouter la clé SSH

1. Allez sur GitHub → Settings > SSH and GPG keys > New SSH Key.
2. Collez la clé et sauvegardez.
3. Ajouter l'URL SSH de votre dépôt comme distant :

## Tester la connexion SSH avec GitHub
Cette commande teste la connexion SSH avec GitHub pour vérifier que tout est bien configuré.

```bash
ssh -T git@github.com
```
Explication des éléments :
- `ssh` : Commande pour se connecter via SSH.
- `-T` : Empêche l'ouverture d'un shell, utilisé pour tester la connexion.
- `git@github.com` : Utilisateur et serveur GitHub.

**Résultat attendu :**
- Si tout est configuré correctement, vous verrez un message similaire à :
  ```
  Hi <utilisateur>! You've successfully authenticated, but GitHub does not provide shell access.
  ```
- Si cela ne fonctionne pas, assurez-vous que votre clé SSH est ajoutée à votre agent et associée à votre compte GitHub.
  
# Collaborer avec son dépôt distant

## Créer un dépôt distant

1. Connectez-vous à GitHub.
2. Cliquez sur le bouton New Repository (Nouveau dépôt).
3. Donnez un nom au dépôt (par exemple, `mon-projet2`).
4. Ne cochez aucune option (pas de README, .gitignore ou licence) pour un dépôt vierge.
5. Cliquez sur Create Repository.

## Créer le repos local et le lier au repos distant

1. Créer un nouveau projet en local nommé `mon-projet2` manuellement ou avec le terminal

```bash
mkdir mon-projet2
```

2. Se replacer sur le dossier projet

```bash
cd ./mon-projet2
```

3. Créer un fichier README

```bash
echo "# test" >> README.md
```

4. Initialiser le dossier avec Git

```bash
git init
```

1. Renommer la branche par défaut en `main` si la branche actuelle est `master`
Cette commande renomme la branche actuelle en "main" pour suivre les conventions modernes.

```bash
git branch -M main
```
Explication des éléments :
- `git branch` : Commande pour travailler avec les branches.
- `-M` : Renomme la branche actuelle en "main".

6. Ajouter le fichier README dans la zone de staging et préparer le commit
   
```bash
git add README.md
git commit -m "first commit"
```

7. Lier votre repos local avec le repos distant

L'origine distante spécifie l'URL d'un dépôt Git distant, comme celui sur GitHub.

```bash
git remote add origin git@github.com:{utilisateur}/mon-projet2.git
```
Explication des éléments :
- `git remote add` : Ajoute un dépôt distant à votre dépôt local.
- `origin` : Nom donné à l'origine distante (standard).
- `git@github.com:<utilisateur>/mon-projet.git` : URL du dépôt distant, avec le nom d'utilisateur GitHub et le nom du projet.

8.  Pousser les modifications vers GitHub
On envoie les modifications locales vers le dépôt distant sur GitHub.

```bash
git push -u origin main
```
Explication des éléments :
- `git push` : Envoie les commits locaux vers un dépôt distant.
- `-u` : Définit origin main comme la branche par défaut pour les futures opérations de git push.
- `origin` : Nom du dépôt distant.
- `main` : Branche à pousser.

9.  Vérifiez votre dépôt sur GitHub
Rendez-vous sur l'URL du dépôt GitHub (https://github.com/<votre-utilisateur>/mon-projet.git) pour voir les fichiers poussés.

10. Afficher les remotes
Cela permet de lister les remotes associées au dépôt, notamment l'origine distante.

```bash
git remote -v
```
Explication des éléments :
- `git remote` : Commande pour gérer les dépôts distants.
- `-v` : Affiche les URL de chaque dépôt distant configuré.

11. Afficher les informations sur l'origine distante
Affiche les détails de l'origine distante, y compris les URL pour fetcher et pousser.

```bash
git remote show origin
```
Explication des éléments :
- `git remote show` : Affiche les informations détaillées sur un dépôt distant.
- `origin` : Nom du dépôt distant.

**Exemple de sortie :**
```
* remote origin
  Fetch URL: git@github.com:utilisateur/mon-projet.git
  Push URL: git@github.com:utilisateur/mon-projet.git
  HEAD branch: main
  Remote branches:
    main tracked
  Local branches configured for 'git pull':
    main merges with remote main
  Local ref configured for 'git push':
    main pushes to main (up to date)
```

# Récapitulatif

| Commande                                 | Description                          |
|------------------------------------------|--------------------------------------|
| `mkdir mon-projet`                       | Crée un dossier nommé "mon-projet". |
| `cd mon-projet`                          | Se déplace dans le dossier "mon-projet". |
| `git init`                               | Initialise un dépôt Git dans le dossier courant. |
| `git config --local user.name "VotreNom"` | Configure le nom d’utilisateur localement pour le dépôt actuel. |
| `git config --local user.email "VotreEmail"` | Configure l’adresse e-mail localement pour le dépôt actuel. |
| `echo "# Mon Projet" > README.md`        | Crée un fichier README.md et y écrit "# Mon Projet". |
| `git add README.md`                      | Ajoute README.md à la zone de staging. |
| `git commit -m "Initial commit: Add README.md"` | Enregistre les modifications avec un message de commit. |
| `ssh-keygen -t rsa -b 4096 -C "votre.email@example.com"` | Génère une clé SSH pour sécuriser la connexion avec GitHub. |
| `eval "$(ssh-agent -s)"`                 | Lance l’agent SSH en arrière-plan. |
| `ssh-add ~/.ssh/toto`                    | Ajoute la clé privée SSH à l’agent pour l’authentification. |
| `cat ~/.ssh/toto.pub`                    | Affiche la clé publique SSH afin de l'ajouter à GitHub. |
| `ssh -T git@github.com`                  | Teste la connexion SSH avec GitHub. |
| `git remote add origin git@github.com:<utilisateur>/mon-projet.git` | Ajoute le dépôt distant GitHub en tant qu'`origin`. |
| `git push -u origin main`                | Pousse les modifications locales sur la branche `main` du dépôt distant. |
| `git branch -M main`                     | Renomme la branche actuelle en `main`. |
| `git push -u origin main`                | Pousse la branche `main` vers le dépôt distant après renommage. |
| `git remote -v`                          | Affiche la liste des dépôts distants configurés. |
| `git remote show origin`                 | Affiche des détails sur le dépôt distant `origin`. |
