# Bandit - Niveau 3 → Niveau 4
## Objectif
Le mot de passe permettant d'accéder au **niveau 4** est stocké dans **un fichier caché** situé dans le répertoire `inhere`.
L'objectif est de localiser ce fichier, puis d'afficher son contenu afin de récupérer le mot de passe du niveau suivant.
---
## Commandes utilisées
- `ls`
- `ls -la`
- `cd`
- `cat`
---
## Étape 1 : Afficher le contenu du répertoire personnel
Lister les fichiers du répertoire personnel :
```bash
ls -la
```
### Résultat
```text
total 24
drwxr-xr-x   3 root root 4096 ...
drwxr-xr-x 150 root root 4096 ...
-rw-r--r--   1 root root  220 .bash_logout
-rw-r--r--   1 root root 3851 .bashrc
-rw-r--r--   1 root root  807 .profile
drwxr-xr-x   2 root root 4096 inhere
```
### Explication
La commande :
```bash
ls -la
```
- `-l` : affiche les informations détaillées des fichiers.
- `-a` : affiche également les fichiers cachés (ceux dont le nom commence par un point `.`).
On remarque un répertoire nommé `inhere`.
---
## Étape 2 : Accéder au répertoire
```bash
cd inhere
```
Vérifier son contenu :
```bash
ls -la
```
Résultat :
```text
total 12
drwxr-xr-x 2 root root 4096 .
drwxr-xr-x 3 root root 4096 ..
-rw-r----- 1 bandit4 bandit3 33 ...Hiding-From-You
```
Le fichier recherché est :
```text
...Hiding-From-You
```
Il est considéré comme caché car son nom commence par un ou plusieurs points (`.`).
---
## Étape 3 : Lire le contenu du fichier
Afficher le contenu du fichier :
```bash
cat ...Hiding-From-You
```
Le terminal affiche alors le mot de passe du niveau suivant. 
---
## Étape 4 : Se connecter au niveau suivant
Quitter la session :
```bash
exit
```
Puis établir une connexion SSH avec l'utilisateur `bandit4` :
```bash
ssh bandit4@bandit.labs.overthewire.org -p 2220
```
Saisir le mot de passe obtenu à l'étape précédente.
---
## Explication des commandes
| Commande | Description |
|----------|-------------|
| `ls` | Liste les fichiers du répertoire courant. |
| `ls -la` | Affiche tous les fichiers, y compris les fichiers cachés, avec leurs détails. |
| `cd inhere` | Accède au répertoire `inhere`. |
| `cat ...Hiding-From-You` | Affiche le contenu du fichier caché. |
| `exit` | Quitte la session SSH. |
| `ssh utilisateur@hôte -p 2220` | Se connecte au niveau suivant. |
---
## Schéma de résolution
```text
Connexion SSH (bandit3)
          │
          ▼
       ls -la
          │
          ▼
       inhere
          │
          ▼
     cd inhere
          │
          ▼
       ls -la
          │
          ▼
...Hiding-From-You
          │
          ▼
cat ...Hiding-From-You
          │
          ▼
 Mot de passe obtenu
          │
          ▼
        exit
          │
          ▼
ssh bandit4@bandit.labs.overthewire.org -p 2220
```
---
## Bonnes pratiques
Sous Linux, les fichiers commençant par un point (`.`) sont masqués par défaut. Pour les afficher, utilisez l'option `-a` de la commande `ls` :
```bash
ls -a
```
ou, pour obtenir des informations détaillées :

```bash
ls -la
```
---