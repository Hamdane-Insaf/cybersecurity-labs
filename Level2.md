# Bandit - Niveau 2 → Niveau 3
## Objectif
Le mot de passe permettant d'accéder au **niveau 3** est stocké dans un fichier nommé :
```text
--spaces in this filename--
```
Ce fichier est situé dans le répertoire personnel de l'utilisateur `bandit2`.
---
## Étape 1 : Vérifier le fichier
Afficher les fichiers du répertoire courant :
```bash
ls
```
Résultat :
```text
--spaces in this filename--
```
---
## Étape 2 : Lire le contenu du fichier
Le nom du fichier contient des espaces. Il faut donc utiliser des guillemets :
```bash
cat "./--spaces in this filename--"
```
ou échapper les espaces :

```bash
cat ./--spaces\ in\ this\ filename--
```
Le contenu affiché est le mot de passe du niveau suivant.
---
## Étape 3 : Se connecter au niveau suivant
Quitter la session :
```bash
exit
```
Puis se connecter au niveau 3 :
```bash
ssh bandit3@bandit.labs.overthewire.org -p 2220
```
Entrer le mot de passe récupéré précédemment.
---
## Explication
Les espaces séparent normalement les arguments d'une commande Linux.
Les guillemets (`" "`) permettent d'indiquer que tout le texte correspond à un **seul nom de fichier**.
Le caractère `\` permet également d'échapper les espaces.
---
## Commandes utilisées
| Commande | Description |
|----------|-------------|
| `ls` | Liste les fichiers du répertoire courant. |
| `cat "--spaces in this filename--"` | Affiche le contenu du fichier. |
| `exit` | Quitte la session SSH. |
| `ssh bandit3@bandit.labs.overthewire.org -p 2220` | Connexion au niveau suivant. |
---
