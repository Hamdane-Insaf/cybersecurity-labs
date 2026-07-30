# Bandit - Niveau 10 → Niveau 11
## Objectif
Le mot de passe permettant d'accéder au **niveau 11** est stocké dans le fichier **`data.txt`**.
L'énoncé précise :
> The password for the next level is stored in the file `data.txt`, which contains base64 encoded data.
Cela signifie que le contenu du fichier est **encodé en Base64**. Le mot de passe n'est donc pas directement lisible. Il faut d'abord **décoder** le contenu du fichier afin d'obtenir le mot de passe.
---
# Problème rencontré
Le fichier **`data.txt`** contient des caractères lisibles, mais ceux-ci représentent des données **encodées en Base64** et non le véritable mot de passe.
Par exemple, un fichier Base64 peut contenir :
```text
SGVsbG8gV29ybGQh
```
Cette chaîne n'est pas le message original. Elle correspond à un texte encodé.
Une lecture avec :
```bash
cat data.txt
```
affiche uniquement les données encodées.
Il faut donc les décoder.
---
# Étape 1 : Vérifier la présence du fichier
Lister les fichiers présents dans le répertoire courant :
```bash
ls
```
### Résultat
```text
data.txt
```
Le fichier contenant le mot de passe est bien présent.
---
# Étape 2 : Observer le contenu du fichier
Afficher le contenu :
```bash
cat data.txt
```
### Résultat
Le terminal affiche une longue chaîne ressemblant à :
```text
VGhlIHBhc3N3b3JkIGlz...
```
Cette chaîne est encodée en Base64.
---
# Étape 3 : Décoder le fichier Base64
Utiliser la commande :
```bash
base64 -d data.txt
```
---
## Explication
La commande **`base64`** permet d'encoder ou de décoder des données au format Base64.
L'option :
```text
-d
```
signifie :
> **decode** (décoder).
Ainsi :
```bash
base64 -d data.txt
```
lit le contenu du fichier, le décode et affiche le texte original.
---
# Comprendre le Base64
Le Base64 est une méthode d'encodage qui transforme des données en caractères ASCII.
Par exemple :
Texte original :
```text
Bonjour
```
Encodage :
```text
Qm9uam91cg==
```
Décodage :
```bash
echo "Qm9uam91cg==" | base64 -d
```
Résultat :
```text
Bonjour
```
Le même principe est utilisé dans ce niveau.
---
# Résultat obtenu
Après avoir exécuté :
```bash
base64 -d data.txt
```
le terminal affiche directement :
```text
Mot_de_passe_du_niveau_suivant
```
Cette chaîne correspond au mot de passe du **niveau 11**.
---
# Étape 4 : Se connecter au niveau suivant
Quitter la session actuelle :
```bash
exit
```
Puis se connecter avec l'utilisateur **bandit11** :
```bash
ssh bandit11@bandit.labs.overthewire.org -p 2220
```
Entrer ensuite le mot de passe obtenu.
---
# Explication des commandes
| Commande | Description |
|----------|-------------|
| `ls` | Affiche les fichiers présents dans le répertoire courant. |
| `cat` | Affiche le contenu d'un fichier. |
| `base64` | Encode ou décode des données au format Base64. |
| `base64 -d` | Décode un fichier encodé en Base64. |
| `exit` | Ferme la connexion SSH actuelle. |
| `ssh` | Permet de se connecter à un serveur distant. |
---
# Schéma de résolution
```text
Connexion SSH (bandit10)
          │
          ▼
         ls
          │
          ▼
      data.txt
          │
          ▼
   cat data.txt
          │
          ▼
 Données encodées Base64
          │
          ▼
 base64 -d data.txt
          │
          ▼
 Mot de passe obtenu
          │
          ▼
        exit
          │
          ▼
ssh bandit11@bandit.labs.overthewire.org -p 2220
```
---
# Bonnes pratiques
- Identifier le type d'encodage avant de tenter de lire un fichier.
- Utiliser `base64 -d` uniquement lorsque les données sont encodées en Base64.
- Vérifier le contenu d'un fichier avec `cat` avant de le traiter.
- Consulter la documentation de la commande avec :
```bash
man base64
```
pour découvrir toutes les options disponibles.