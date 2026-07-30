# Bandit - Niveau 6 → Niveau 7
## Objectif
Le mot de passe permettant d'accéder au **niveau 7** est stocké **quelque part sur le système**.
Le fichier recherché possède les propriétés suivantes :
- appartient à l'utilisateur **bandit7** ;
- appartient au groupe **bandit6** ;
- a une taille exacte de **33 octets**.
L'objectif est de retrouver ce fichier, puis d'afficher son contenu.
---
## Problème rencontré
Le fichier n'est pas situé dans le répertoire personnel de l'utilisateur, mais **quelque part sur le système de fichiers**.
Il serait impossible de parcourir tous les répertoires manuellement. La commande **`find`** permet d'effectuer une recherche en utilisant plusieurs critères, tels que le propriétaire, le groupe et la taille du fichier.
---
## Commandes utilisées
- `find`
- `cat`
---
## Étape 1 : Rechercher le fichier
Exécuter la commande suivante :
```bash
find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
```
### Explication
- `find /` : lance une recherche à partir de la racine (`/`) du système.
- `-user bandit7` : recherche les fichiers appartenant à l'utilisateur **bandit7**.
- `-group bandit6` : recherche les fichiers appartenant au groupe **bandit6**.
- `-size 33c` : recherche les fichiers dont la taille est exactement de **33 octets** (`c` signifie *bytes* ou octets).
- `2>/dev/null` : masque les messages d'erreur tels que **Permission denied** afin de n'afficher que les résultats utiles.
Exemple de résultat :
```text
/var/lib/dpkg/info/bandit7.password
```
---
## Étape 2 : Lire le contenu du fichier
Une fois le fichier trouvé, afficher son contenu :
```bash
cat /var/lib/dpkg/info/bandit7.password
```
Le terminal affiche alors le mot de passe du niveau suivant.
---
## Étape 3 : Se connecter au niveau suivant
Quitter la session actuelle :
```bash
exit
```
Puis se connecter avec l'utilisateur **bandit7** :
```bash
ssh bandit7@bandit.labs.overthewire.org -p 2220
```
Entrer le mot de passe obtenu à l'étape précédente.
---
## Explication des commandes
| Commande | Description |
|----------|-------------|
| `find / -user bandit7 -group bandit6 -size 33c 2>/dev/null` | Recherche un fichier appartenant à **bandit7**, au groupe **bandit6** et de **33 octets**, tout en masquant les messages d'erreur. |
| `cat chemin_du_fichier` | Affiche le contenu du fichier trouvé. |
| `exit` | Quitte la session SSH. |
| `ssh bandit7@bandit.labs.overthewire.org -p 2220` | Se connecte au niveau suivant. |
---
## Schéma de résolution
```text
Connexion SSH (bandit6)
          │
          ▼
Recherche avec find
          │
          ▼
find /
-user bandit7
-group bandit6
-size 33c
2>/dev/null
          │
          ▼
Fichier trouvé
          │
          ▼
cat chemin_du_fichier
          │
          ▼
Mot de passe obtenu
          │
          ▼
        exit
          │
          ▼
ssh bandit7@bandit.labs.overthewire.org -p 2220
```
---
## Compétences acquises
À la fin de ce niveau, vous savez :
- rechercher un fichier dans l'ensemble du système avec **`find`** ;
- filtrer une recherche selon le **propriétaire** d'un fichier ;
- filtrer selon le **groupe** ;
- rechercher un fichier selon sa **taille** ;
- rediriger les messages d'erreur avec **`2>/dev/null`**.
---
## Bonnes pratiques
Lorsque vous lancez une recherche depuis la racine (`/`), il est normal que certains répertoires soient inaccessibles avec votre compte. L'utilisation de **`2>/dev/null`** permet de masquer ces messages d'erreur et d'obtenir une sortie plus lisible.
La commande **`find`** est l'un des outils les plus puissants de Linux pour rechercher des fichiers selon leurs métadonnées (propriétaire, groupe, taille, permissions, date, etc.).
---