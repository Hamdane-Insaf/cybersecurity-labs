# Bandit - Niveau 8 → Niveau 9
## Objectif
Le mot de passe permettant d'accéder au **niveau 9** est stocké dans le fichier **`data.txt`**.
L'énoncé précise :
> The password for the next level is stored in the file `data.txt` and is the only line of text that occurs only once.
Cela signifie que le mot de passe correspond à **l'unique ligne du fichier qui apparaît une seule fois**.

L'objectif est donc d'identifier cette ligne unique parmi toutes les lignes répétées.
---
## Problème rencontré

Le fichier **`data.txt`** contient un grand nombre de lignes.
La majorité des lignes sont présentes plusieurs fois, tandis qu'une seule ligne apparaît une seule fois.
Une recherche manuelle avec :
```bash
cat data.txt
```
serait inefficace car le fichier contient beaucoup de données.
Il faut donc utiliser des commandes permettant de trier et de détecter les doublons.
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
# Étape 2 : Trier le contenu du fichier
Utiliser la commande :
```bash
sort data.txt
```
## Explication
La commande `sort` permet de trier les lignes d'un fichier.
Elle est nécessaire car la commande `uniq` ne détecte les répétitions que lorsque les lignes identiques sont placées côte à côte.
Exemple :
Avant le tri :
```text
abc
xyz
abc
```
Après :
```bash
sort fichier.txt
```
Résultat :
```text
abc
abc
xyz
```
Les lignes identiques sont maintenant regroupées.
---
# Étape 3 : Trouver la ligne unique
Utiliser :
```bash
sort data.txt | uniq -u
```
## Explication
Cette commande combine deux outils grâce au symbole **pipe (`|`)**.
### Partie 1 :
```bash
sort data.txt
```
Trie toutes les lignes du fichier.
### Partie 2 :
```bash
uniq -u
```
Affiche uniquement les lignes qui apparaissent une seule fois.
L'option :
```bash
-u
```
signifie :
> afficher uniquement les lignes uniques.
---
# Comprendre le pipe `|`
Le symbole `|` permet d'envoyer le résultat d'une commande vers une autre commande.
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
sort data.txt
        │
        ▼
Lignes triées
        │
        ▼
uniq -u
        │
        ▼
Ligne présente une seule fois
```
---
# Résultat obtenu
La commande :
```bash
sort data.txt | uniq -u
```
affiche une seule ligne.
Cette ligne correspond au :
```
Mot de passe du niveau suivant
```
---
# Étape 4 : Se connecter au niveau suivant
Quitter la session actuelle :
```bash
exit
```
Puis se connecter avec l'utilisateur **bandit9** :
```bash
ssh bandit9@bandit.labs.overthewire.org -p 2220
```
Entrer ensuite le mot de passe trouvé précédemment.
---
# Explication des commandes
| Commande | Description |
|----------|-------------|
| `ls` | Affiche les fichiers présents dans le répertoire courant. |
| `sort` | Trie les lignes d'un fichier. |
| `uniq` | Recherche ou supprime les lignes répétées. |
| `uniq -u` | Affiche uniquement les lignes présentes une seule fois. |
| `|` | Envoie la sortie d'une commande vers une autre. |
| `exit` | Ferme la connexion SSH actuelle. |
| `ssh` | Permet de se connecter à un serveur distant. |
---
# Schéma de résolution
```text
Connexion SSH (bandit8)
          │
          ▼
         ls
          │
          ▼
      data.txt
          │
          ▼
  sort data.txt
          │
          ▼
Lignes triées
          │
          ▼
    uniq -u
          │
          ▼
 Ligne unique
          │
          ▼
 Mot de passe obtenu
          │
          ▼
        exit
          │
          ▼
ssh bandit9@bandit.labs.overthewire.org -p 2220
```
---
# Bonnes pratiques
- Utiliser `sort` avant `uniq` lorsque les doublons ne sont pas regroupés.
- Utiliser les pipes (`|`) pour construire des chaînes de commandes Linux efficaces.
- Lire les manuels des commandes avec :
```bash
man sort
```
et :
```bash
man uniq
```
pour découvrir les options disponibles.
---