# Bandit - Niveau 7 → Niveau 8
## Objectif
Le mot de passe permettant d'accéder au **niveau 8** est stocké dans le fichier **`data.txt`**, à côté du mot **`millionth`**.
L'objectif est de retrouver cette ligne afin de récupérer le mot de passe du niveau suivant.
---
## Problème
Le fichier **`data.txt`** contient un très grand nombre de lignes. Rechercher le mot de passe manuellement serait long et inefficace.
Il est donc préférable d'utiliser une commande permettant de rechercher automatiquement une ligne contenant un mot précis.
---
## Étape 1 : Vérifier la présence du fichier
Lister les fichiers du répertoire courant :
```bash
ls
```
### Résultat
```text
data.txt
```
---
## Étape 2 : Rechercher le mot **millionth**
Utiliser la commande suivante :
```bash
grep "millionth" data.txt
```
### Explication
- `grep` : recherche un texte dans un fichier.
- `"millionth"` : mot recherché.
- `data.txt` : fichier dans lequel effectuer la recherche.
La commande affiche uniquement la ligne contenant le mot **millionth**.
### Exemple de résultat
```text
millionth cvX2JJa4CFALtqS87jk27qwqGhBM9plV
```
Le texte situé après **millionth** correspond au **mot de passe du niveau suivant**.
---
## Pourquoi utiliser `grep` ?
La commande `grep` est conçue pour rechercher rapidement un mot ou une expression dans un ou plusieurs fichiers.
Au lieu de parcourir manuellement des milliers de lignes, `grep` affiche directement celles qui contiennent le mot recherché.
Ainsi :
```bash
grep "millionth" data.txt
```
signifie :
> Rechercher toutes les lignes contenant le mot **millionth** dans le fichier **data.txt**.
---
## Étape 3 : Se connecter au niveau suivant
Quitter la session actuelle :
```bash
exit
```
Puis se connecter avec l'utilisateur **bandit8** :
```bash
ssh bandit8@bandit.labs.overthewire.org -p 2220
```
Lorsque le terminal demande le mot de passe, saisir celui obtenu à l'étape précédente.
---
## Explication des commandes
| Commande | Description |
|----------|-------------|
| `ls` | Affiche les fichiers et dossiers du répertoire courant. |
| `grep "millionth" data.txt` | Recherche la ligne contenant le mot **millionth** dans le fichier `data.txt`. |
| `exit` | Ferme la session SSH actuelle. |
| `ssh bandit8@bandit.labs.overthewire.org -p 2220` | Établit une connexion SSH vers le niveau suivant. |
---
## Schéma de résolution

```text
Connexion SSH (bandit7)
          │
          ▼
         ls
          │
          ▼
      data.txt
          │
          ▼
grep "millionth" data.txt
          │
          ▼
 Ligne contenant "millionth"
          │
          ▼
 Mot de passe obtenu
          │
          ▼
        exit
          │
          ▼
ssh bandit8@bandit.labs.overthewire.org -p 2220
```
---
## Bonnes pratiques
- Utiliser **`grep`** pour rechercher rapidement un mot dans un fichier volumineux.
- Consulter la documentation avec :
```bash
man grep
```
pour découvrir les nombreuses options de cette commande.
- Éviter de parcourir un gros fichier manuellement lorsqu'un outil de recherche est disponible.
---