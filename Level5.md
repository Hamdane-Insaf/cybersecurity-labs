# Bandit - Niveau 5 → Niveau 6

## Objectif

Le mot de passe permettant d'accéder au **niveau 6** est stocké dans un fichier situé quelque part dans le répertoire **`inhere`**.

Le fichier recherché possède les caractéristiques suivantes :

- il est **lisible par un humain** ;
- sa taille est exactement de **1033 octets** ;
- il **n'est pas exécutable**.

L'objectif est de retrouver ce fichier puis d'afficher son contenu.

---

## Problème rencontré

Le répertoire `inhere` contient plusieurs sous-répertoires et un grand nombre de fichiers.

Il serait très long de vérifier chaque fichier manuellement. La commande **`find`** permet de rechercher automatiquement un fichier selon plusieurs critères (taille, permissions, type, etc.).

---

## Commandes utilisées

- `cd`
- `find`
- `cat`

---

## Étape 1 : Accéder au répertoire

Depuis le répertoire personnel :

```bash
cd inhere
```
---
## Étape 2 : Rechercher le fichier
Exécuter la commande suivante :
```bash
find . -type f -readable -size 1033c ! -executable
```
### Explication
- `find .` : recherche à partir du répertoire courant.
- `-type f` : recherche uniquement les fichiers.
- `-readable` : sélectionne les fichiers lisibles.
- `-size 1033c` : sélectionne les fichiers de **1033 octets** (`c` signifie *bytes* ou octets).
- `! -executable` : exclut les fichiers exécutables.
Exemple de résultat :
```text
./maybehere07/.file2
```
> **Remarque :** Le chemin obtenu peut être différent selon la version du challenge. Utilisez toujours celui renvoyé par la commande `find`.
---
## Étape 3 : Lire le contenu du fichier
Une fois le fichier trouvé, afficher son contenu :
```bash
cat ./maybehere07/.file2
```
Le terminal affiche alors le mot de passe du niveau suivant.
---
## Étape 4 : Se connecter au niveau suivant
Quitter la session actuelle :
```bash
exit
```
Puis se connecter avec l'utilisateur **bandit6** :

```bash
ssh bandit6@bandit.labs.overthewire.org -p 2220
```
Entrer le mot de passe obtenu à l'étape précédente.
---
## Explication des commandes
| Commande | Description |
|----------|-------------|
| `cd inhere` | Accède au répertoire `inhere`. |
| `find . -type f -readable -size 1033c ! -executable` | Recherche un fichier répondant aux critères demandés. |
| `cat chemin_du_fichier` | Affiche le contenu du fichier trouvé. |
| `exit` | Quitte la session SSH. |
| `ssh bandit6@bandit.labs.overthewire.org -p 2220` | Se connecte au niveau suivant. |
---
## Schéma de résolution
```text
Connexion SSH (bandit5)
          │
          ▼
     cd inhere
          │
          ▼
 Recherche avec find
          │
          ▼
find . -type f
     -readable
     -size 1033c
     ! -executable
          │
          ▼
 Fichier correspondant
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
ssh bandit6@bandit.labs.overthewire.org -p 2220
```
---
## Compétences acquises
À la fin de ce niveau, vous savez :
- utiliser la commande **`find`** pour rechercher des fichiers ;
- filtrer les fichiers selon leur **type** ;
- rechercher un fichier selon sa **taille** ;
- vérifier les **permissions** d'un fichier (lisible, exécutable) ;
- combiner plusieurs critères dans une seule commande.
---
## Bonnes pratiques
La commande **`find`** est l'un des outils les plus puissants de Linux pour rechercher des fichiers. Elle permet de combiner plusieurs critères (nom, taille, permissions, date de modification, propriétaire, etc.) afin de localiser rapidement un fichier précis, même dans une arborescence contenant des centaines de répertoires.
---