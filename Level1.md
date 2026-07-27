# Bandit - Niveau 1 → Niveau 2
## Objectif
Le mot de passe permettant d'accéder au **niveau 2** est stocké dans un fichier nommé **`-`** (un simple tiret), situé dans le répertoire personnel de l'utilisateur `bandit1`.
L'objectif est de lire le contenu de ce fichier afin de récupérer le mot de passe du niveau suivant.
---
## Problème rencontré
Le fichier s'appelle **`-`**, ce qui peut poser un problème.
Sous Linux, le caractère `-` est généralement interprété comme une **option** d'une commande (par exemple `ls -l` ou `cat -n`). Si l'on exécute directement :
```bash
cat -
```
la commande attend une entrée au clavier (entrée standard) au lieu d'ouvrir le fichier.
Il faut donc indiquer explicitement que `-` est un nom de fichier.
---
## Étape 1 : Vérifier la présence du fichier
Lister les fichiers du répertoire courant :
```bash
ls
```
### Résultat
```text
-
```
---
## Étape 2 : Lire le contenu du fichier
Pour lire le fichier, utiliser :
```bash
cat ./-
```
### Explication
- `.` représente le répertoire courant.
- `./-` indique que `-` est un **nom de fichier** et non une option.
La commande `cat` affiche alors le contenu du fichier, qui correspond au **mot de passe du niveau suivant**.
---
## Pourquoi utiliser `./` ?
En Bash :
- `-` est souvent interprété comme une option.
- `./` signifie **dans le répertoire courant**.
Ainsi :
```bash
cat ./-
```
est interprété comme :
> Lire le fichier nommé `-` situé dans le répertoire courant.
---
## Étape 3 : Se connecter au niveau suivant
Quitter la session actuelle :
```bash
exit
```
Puis se connecter avec l'utilisateur `bandit2` :
```bash
ssh bandit2@bandit.labs.overthewire.org -p 2220
```
Lorsque le terminal demande le mot de passe, saisir celui obtenu avec la commande précédente.
---
## Explication des commandes
| Commande | Description |
|----------|-------------|
| `ls` | Affiche les fichiers et dossiers du répertoire courant. |
| `cat ./-` | Affiche le contenu du fichier nommé `-`. |
| `exit` | Ferme la session SSH actuelle. |
| `ssh utilisateur@hôte -p 2220` | Établit une connexion SSH vers le niveau suivant. |
---
## Schéma de résolution
```text
Connexion SSH (bandit1)
          │
          ▼
         ls
          │
          ▼
          -
          │
          ▼
      cat ./-
          │
          ▼
 Mot de passe obtenu
          │
          ▼
        exit
          │
          ▼
ssh bandit2@bandit.labs.overthewire.org -p 2220
```
---
## Bonnes pratiques
Lorsque le nom d'un fichier contient des caractères spéciaux (`-`, espaces, `*`, `?`, etc.), il est préférable de préciser son chemin (`./nom_du_fichier`) ou d'utiliser des guillemets afin d'éviter toute ambiguïté.
---