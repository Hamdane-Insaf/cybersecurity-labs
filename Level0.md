# Bandit - Niveau 0
## Objectif
Le but de ce premier niveau est de se connecter au serveur **Bandit** en utilisant le protocole **SSH (Secure Shell)**.
Une fois connecté, le joueur pourra accéder au niveau suivant.
---
## Informations de connexion

| Élément | Valeur |
|---------|--------|
| Hôte | `bandit.labs.overthewire.org` |
| Port | `2220` |
| Utilisateur | `bandit0` |
| Mot de passe | `bandit0` |
---
## Qu'est-ce que SSH ?
SSH (**Secure Shell**) est un protocole réseau qui permet d'établir une connexion sécurisée entre un client et un serveur distant.
Il est principalement utilisé pour :
- administrer un serveur Linux à distance ;
- exécuter des commandes sur une machine distante ;
- transférer des fichiers de manière sécurisée.
---
## Commande utilisée
```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```
### Explication de la commande

| Élément | Description |
|---------|-------------|
| `ssh` | Lance le client SSH. |
| `bandit0` | Nom de l'utilisateur. |
| `@` | Sépare le nom d'utilisateur du serveur. |
| `bandit.labs.overthewire.org` | Adresse du serveur Bandit. |
| `-p` | Permet de préciser un port différent du port SSH par défaut (22). |
| `2220` | Port utilisé par le serveur Bandit. |
---
## Authentification
Après avoir exécuté la commande, le terminal demande le mot de passe :
```text
bandit0@bandit.labs.overthewire.org's password:
```
Saisir :
```text
bandit0
```
## Connexion réussie
Si les informations sont correctes, le terminal affiche un message de bienvenue similaire à celui-ci :

```text
Welcome to OverTheWire!
bandit0@bandit:~$
```
L'utilisateur est maintenant connecté au serveur et peut exécuter des commandes Linux.
---
## Résultat
À la fin de ce niveau :
- la connexion SSH est établie avec succès ;
- l'utilisateur accède au compte `bandit0` ;
---
# Bandit - Niveau 0 → Niveau 1
## Objectif
Le mot de passe permettant d'accéder au **niveau 1** est stocké dans un fichier nommé **`readme`**, situé dans le répertoire personnel de l'utilisateur `bandit0`.
L'objectif est de retrouver ce mot de passe puis de l'utiliser pour se connecter au niveau suivant (`bandit1`) via SSH.
---
## Commandes utilisées
- `ls` , `cat`
---
## Étape 1 : Afficher le contenu du répertoire
Après la connexion au serveur avec l'utilisateur `bandit0`, afficher les fichiers présents dans le répertoire courant :
```bash
ls
```
### Résultat
```text
readme
```
---
## Étape 2 : Lire le contenu du fichier
Afficher le contenu du fichier `readme` :
```bash
cat readme
```
### Résultat
```text
Congratulations on your first steps into the bandit game!!
Please make sure you have read the rules at https://overthewire.org/rules/
If you are following a course, workshop, walkthrough or other educational activity,
please inform the instructor about the rules as well and encourage them to
contribute to the OverTheWire community so we can keep these games free!
The password you are looking for is: **password**
```
---
## Étape 3 : Se connecter au niveau suivant
Une fois le mot de passe récupéré, quitter la session actuelle :
```bash
exit
```
Puis se connecter avec l'utilisateur `bandit1` :
```bash
ssh bandit1@bandit.labs.overthewire.org -p 2220
```
Lorsque le terminal demande le mot de passe :
Saisir le mot de passe obtenu dans le fichier `readme`
---
## Explication des commandes
| Commande | Description |
|----------|-------------|
| `ls` | Affiche la liste des fichiers et dossiers du répertoire courant. |
| `cat fichier` | Affiche le contenu d'un fichier texte. |
| `exit` | Ferme la session SSH en cours. |
| `ssh utilisateur@hôte -p 2220` | Établit une connexion SSH vers le niveau suivant. |
---
## Schéma de résolution

```text
Connexion SSH (bandit0)
          │
          ▼
        ls
          │
          ▼
      readme
          │
          ▼
    cat readme
          │
          ▼
 Mot de passe obtenu
          │
          ▼
 exit
          │
          ▼
ssh bandit1@bandit.labs.overthewire.org -p 2220
```
---