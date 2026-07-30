# Bandit - Niveau 9 → Niveau 10
## Objectif
Le mot de passe permettant d'accéder au **niveau 10** est stocké dans le fichier **`data.txt`**.
L'énoncé précise :
> The password for the next level is stored in the file `data.txt` in one of the few human-readable strings, preceded by several '=' characters.
Cela signifie que le fichier contient principalement des données **binaires** (non lisibles), mais qu'il existe quelques chaînes de caractères lisibles par un humain. Le mot de passe est l'une de ces chaînes et est précédé de plusieurs caractères `=`.
L'objectif est donc :
1. Extraire uniquement les chaînes lisibles du fichier.
2. Rechercher celle qui commence par plusieurs caractères `=`.
---
# Problème rencontré
Le fichier **`data.txt`** n'est pas un simple fichier texte.
Si l'on exécute :
```bash
cat data.txt
```
le terminal affiche une grande quantité de caractères incompréhensibles, car le fichier contient des données binaires.
Exemple :
```text
�3��T�J�������H��=���...
```
Une recherche manuelle est donc impossible.
Il faut utiliser des commandes capables d'extraire uniquement les parties lisibles du fichier.
---
# Étape 1 : Vérifier la présence du fichier
Lister les fichiers du répertoire courant :
```bash
ls
```
### Résultat
```text
data.txt
```
Le fichier contenant les données est bien présent.
---
# Étape 2 : Observer le contenu du fichier
Afficher le contenu :
```bash
cat data.txt
```
### Résultat
Le résultat contient principalement des caractères illisibles.
Cela indique que le fichier est binaire.
---
# Étape 3 : Extraire les chaînes lisibles
Utiliser la commande :
```bash
strings data.txt
```
## Explication
La commande **`strings`** extrait uniquement les suites de caractères ASCII lisibles présentes dans un fichier.
Par exemple, si un fichier contient :
```text
����Bonjour����Linux����12345����
```
la commande :
```bash
strings fichier
```
affichera :
```text
Bonjour
Linux
12345
```
Dans notre cas, cette commande permet de supprimer tout le contenu binaire inutile.
---
# Étape 4 : Rechercher la chaîne précédée de '='
Utiliser :
```bash
strings data.txt | grep "^==="
```
## Explication
Cette commande combine **`strings`** et **`grep`** grâce au symbole **pipe (`|`)**.
### Partie 1
```bash
strings data.txt
```
Extrait toutes les chaînes lisibles du fichier.
### Partie 2
```bash
grep "^==="
```
Recherche uniquement les lignes qui commencent par plusieurs caractères `=`.
Le symbole :
```text
^
```
signifie :
> début de ligne.
Ainsi :
```bash
grep "^==="
```
signifie :
> afficher uniquement les lignes dont le début est constitué de plusieurs caractères `=`.
Par exemple :
```text
Bonjour
===abc123
Linux
====MotDePasse
Test
```
La commande affichera :
```text
===abc123
====MotDePasse
```
---
# Comprendre le pipe `|`
Le symbole `|` permet d'envoyer le résultat d'une commande vers une autre.
Exemple :
```bash
commande1 | commande2
```
Fonctionnement :
```text
Commande 1
     │
     ▼
Résultat intermédiaire
     │
     ▼
Commande 2
     │
     ▼
Résultat final
```
Dans notre cas :
```text
strings data.txt
        │
        ▼
Chaînes lisibles
        │
        ▼
grep "^==="
        │
        ▼
Chaîne commençant par ===
```
---
# Résultat obtenu
La commande :
```bash
strings data.txt | grep "^==="
```
renvoie une ligne semblable à :
```text
==========mot_de_passe
```
Le mot de passe correspond au texte situé **après les caractères `=`**.
Par exemple :
```text
==========7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4
```
Le mot de passe est :
```text
7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4
```
---
# Étape 5 : Se connecter au niveau suivant
Quitter la session actuelle :
```bash
exit
```
Puis se connecter avec l'utilisateur **bandit10** :
```bash
ssh bandit10@bandit.labs.overthewire.org -p 2220
```
Entrer ensuite le mot de passe obtenu.
---
# Explication des commandes
| Commande | Description |
|----------|-------------|
| `ls` | Affiche les fichiers du répertoire courant. |
| `cat` | Affiche le contenu d'un fichier. |
| `strings` | Extrait les chaînes de caractères lisibles d'un fichier binaire. |
| `grep` | Recherche un texte correspondant à un motif. |
| `grep "^==="` | Recherche les lignes qui commencent par plusieurs caractères `=`. |
| `|` | Envoie la sortie d'une commande vers une autre. |
| `exit` | Ferme la connexion SSH actuelle. |
| `ssh` | Permet de se connecter à un serveur distant. |
---
# Schéma de résolution
```text
Connexion SSH (bandit9)
          │
          ▼
         ls
          │
          ▼
      data.txt
          │
          ▼
 strings data.txt
          │
          ▼
 Chaînes lisibles
          │
          ▼
grep "^==="
          │
          ▼
 Ligne contenant ======
          │
          ▼
 Mot de passe obtenu
          │
          ▼
        exit
          │
          ▼
ssh bandit10@bandit.labs.overthewire.org -p 2220
```
---
# Bonnes pratiques
- Utiliser `strings` lorsqu'un fichier semble contenir des données binaires.
- Utiliser `grep` avec des expressions régulières (`^`, `$`, etc.) pour rechercher des motifs précis.
- Combiner plusieurs commandes avec le pipe (`|`) afin d'effectuer des traitements successifs.
- Consulter la documentation des commandes avec :
```bash
man strings
```
et
```bash
man grep
```
pour découvrir toutes les options disponibles.