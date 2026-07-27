# Bandit - Niveau 4 → Niveau 5
## Objectif
Le mot de passe permettant d'accéder au **niveau 5** est stocké dans **le seul fichier lisible par un humain** situé dans le répertoire **`inhere`**.
L'objectif est d'identifier ce fichier, puis d'afficher son contenu.
---
## Problème rencontré
Le répertoire **`inhere`** contient plusieurs fichiers dont le contenu est inconnu.
Certains sont des fichiers binaires (non lisibles par un humain), tandis qu'un seul est un fichier texte lisible. Pour identifier ce fichier, on utilise la commande **`file`**, qui permet de déterminer le type de chaque fichier.
---
## Commandes utilisées
- `cd`
- `ls`
- `file`
- `cat`
---
## Étape 1 : Accéder au répertoire
Depuis le répertoire personnel :
```bash
cd inhere
```
---
## Étape 2 : Afficher les fichiers
Lister les fichiers présents :
```bash
ls
```
Exemple de résultat :
```text
-file00
-file01
-file02
-file03
-file04
-file05
-file06
-file07
-file08
-file09
```
---
## Étape 3 : Identifier le fichier lisible
Exécuter la commande suivante :
```bash
file ./*
```
### Explication
- `file` : détermine le type d'un fichier.
- `./*` : sélectionne tous les fichiers du répertoire courant.
- `./` est utilisé car les noms des fichiers commencent par un tiret (`-`), ce qui évite que celui-ci soit interprété comme une option.
Exemple de résultat :
```text
./-file00: data
./-file01: data
./-file02: ASCII text
./-file03: data
./-file04: data
...
```
Le fichier identifié comme **`ASCII text`** (ou **texte lisible**) est celui qui contient le mot de passe.
---
## Étape 4 : Lire le contenu du fichier
Afficher le contenu du fichier identifié :
```bash
cat ./-file02
```
> **Remarque :** Le nom du fichier (`-file02` dans cet exemple) peut être différent. Utilisez toujours celui que la commande `file` indique comme étant un fichier texte (`ASCII text`).
Le terminal affiche alors le mot de passe du niveau suivant.
---
## Étape 5 : Se connecter au niveau suivant
Quitter la session actuelle :
```bash
exit
```
Puis se connecter avec l'utilisateur **bandit5** :
```bash
ssh bandit5@bandit.labs.overthewire.org -p 2220
```
Entrer le mot de passe obtenu à l'étape précédente.
---
## Explication des commandes
| Commande | Description |
|----------|-------------|
| `cd inhere` | Accède au répertoire `inhere`. |
| `ls` | Affiche les fichiers du répertoire courant. |
| `file ./*` | Détermine le type de chaque fichier. |
| `cat ./nom_du_fichier` | Affiche le contenu du fichier identifié comme texte. |
| `exit` | Quitte la session SSH. |
| `ssh bandit5@bandit.labs.overthewire.org -p 2220` | Se connecte au niveau suivant. |
---
## Schéma de résolution
```text
Connexion SSH (bandit4)
          │
          ▼
     cd inhere
          │
          ▼
         ls
          │
          ▼
 Plusieurs fichiers
          │
          ▼
      file ./*
          │
          ▼
 Identifier le fichier
 de type "ASCII text"
          │
          ▼
cat ./nom_du_fichier
          │
          ▼
 Mot de passe obtenu
          │
          ▼
        exit
          │
          ▼
ssh bandit5@bandit.labs.overthewire.org -p 2220
```
---
## Compétences acquises
À la fin de ce niveau, vous savez :
- utiliser la commande **`file`** pour identifier le type d'un fichier ;
- distinguer un fichier texte d'un fichier binaire ;
- utiliser le caractère générique **`*`** pour sélectionner plusieurs fichiers ;
- comprendre l'intérêt du préfixe **`./`** lorsque les noms de fichiers commencent par un tiret (`-`) ;
- afficher le contenu d'un fichier avec **`cat`**.
---
## Bonnes pratiques
Avant d'ouvrir un fichier inconnu, il est recommandé d'utiliser la commande **`file`** afin d'identifier son type. Cette commande permet de savoir rapidement s'il s'agit d'un fichier texte, d'un exécutable, d'une image, d'une archive ou d'un fichier binaire.
Lorsque les noms de fichiers commencent par un tiret (`-`), utilisez le préfixe **`./`** pour éviter que le shell n'interprète le nom comme une option de commande.
---