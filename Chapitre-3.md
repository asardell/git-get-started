# Travailler avec les commit

1. [Travailler avec les commit](#travailler-avec-les-commit)
   1. [1. Utilisation de `git add`](#1-utilisation-de-git-add)
      1. [1.1 `git add .` : Ajouter tous les fichiers modifiés](#11-git-add---ajouter-tous-les-fichiers-modifiés)
      2. [1.2 git add -p : Ajouter des parties spécifiques des modifications](#12-git-add--p--ajouter-des-parties-spécifiques-des-modifications)
      3. [1.3 git add -p  : Sélectionner les modifications d'un seul fichier](#13-git-add--p---sélectionner-les-modifications-dun-seul-fichier)
   2. [2. Modifier un commit avec git commit --amend](#2-modifier-un-commit-avec-git-commit---amend)
      1. [2.1 Modifier le message d'un commit](#21-modifier-le-message-dun-commit)
      2. [2.2 Ajouter un fichier oublié à un commit](#22-ajouter-un-fichier-oublié-à-un-commit)
      3. [2.3 Modifier un commit déjà poussé (⚠️ avec précaution)](#23-modifier-un-commit-déjà-poussé-️-avec-précaution)
   3. [Conclusion](#conclusion)

Dans ce chapitre, nous allons voir comment gérer efficacement les ajouts et modifications de fichiers dans Git.  

## 1. Utilisation de `git add`

Avant d'envoyer des modifications à un dépôt distant, il faut les ajouter à la zone de staging. Git propose plusieurs méthodes pour cela.

### 1.1 `git add .` : Ajouter tous les fichiers modifiés
La commande suivante ajoute **toutes** les modifications présentes dans le projet :  

```bash
git add .
```

Exemple d'utilisation :

Modifions un fichier et créons-en un autre :

```bash
echo "Nouvelle ligne" >> fichier1.txt
echo "Nouveau fichier" > fichier2.txt
```
Vérifions les modifications :

```bash
git status
```

Ajoutons toutes les modifications :

```bash
git add .
```
Vérifions que les fichiers sont bien en staging :

```bash
git status
```

### 1.2 git add -p : Ajouter des parties spécifiques des modifications

Parfois, on ne veut ajouter qu'une partie des modifications d'un fichier. Pour cela, on utilise la commande patch :

```bash
git add -p
```
Cela ouvre une interface interactive où Git affiche chaque modification par section (hunk) et demande ce que vous voulez en faire :

|Option |Signification|
|-------|------------------|
|y  	|Ajouter ce hunk |
|n      |Ne pas l'ajouter|
|s      |Diviser le hunk en morceaux plus petits|
|q      |Quitter sans ajouter|
|-------|-----------|

Exemple d'utilisation :

Modifions un fichier existant :

```bash
echo "Première modification" >> fichier1.txt
echo "Deuxième modification" >> fichier1.txt
```
Vérifions les modifications :

```bash
git diff
```
Ajoutons les changements interactifs :

```bash
git add -p
```
Sélectionnons seulement la première modification (y pour accepter, n pour refuser la deuxième).

Vérifions les fichiers en staging :

```bash
git status
```

### 1.3 git add -p <fichier> : Sélectionner les modifications d'un seul fichier
Si vous voulez appliquer git add -p sur un fichier spécifique, utilisez :

```bash
git add -p fichier1.txt
```
Cela fonctionne de la même manière, mais uniquement sur le fichier ciblé.

## 2. Modifier un commit avec git commit --amend

Si vous avez fait un commit mais que vous devez le modifier, utilisez git commit --amend.

### 2.1 Modifier le message d'un commit
Si vous venez de faire un commit et que vous voulez changer son message :

```bash
git commit --amend
```
Cela ouvre un éditeur où vous pouvez modifier le message.

Exemple :

```bash
git commit -m "Premier commit"
git commit --amend
```
Modifiez le message et sauvegardez.

### 2.2 Ajouter un fichier oublié à un commit
Si vous avez oublié d'ajouter un fichier dans votre dernier commit :

Ajoutez le fichier :

```bash
git add fichier_oublie.txt
```
Amendez le commit :

```bash
git commit --amend --no-edit
```
L'option --no-edit garde le message de commit existant.

### 2.3 Modifier un commit déjà poussé (⚠️ avec précaution)
Si le commit a déjà été poussé à un dépôt distant, vous devez forcer le push :

```bash
git push --force
```
⚠️ Attention ! Cela peut causer des problèmes si d'autres personnes ont déjà récupéré ce commit.

## Conclusion
|Commande	|Description|
----------- |------------|
|git add .	|Ajoute tous les fichiers modifiés|
|git add -p	|Ajoute des parties spécifiques des modifications|
|git add -p <fichier>|	Sélectionne les modifications d'un fichier donné|
|git commit --amend	|Modifie le dernier commit|
|git commit --amend --no-edit	|Ajoute des fichiers au dernier commit sans modifier son message|
|git push --force	Force la mise à jour d'un commit déjà poussé (à utiliser avec prudence)|