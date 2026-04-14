# Git & GitHub — Documentation

## C'est quoi Git et GitHub ?

Quand on code, on modifie des fichiers en permanence. Sans outil dédié, il est très facile de casser quelque chose qui marchait, de perdre une ancienne version, ou de ne pas savoir ce qui a changé entre hier et aujourd'hui.

**Git** est un outil qui résout ce problème. Il garde en mémoire toutes les versions de ton code, comme un historique ultra-précis. Tu peux à tout moment voir ce qui a changé, revenir en arrière, ou travailler en parallèle sur plusieurs idées sans risquer de tout mélanger. Git fonctionne **en local**, sur ta machine.

**GitHub** est un site web qui héberge ton code en ligne. Il te permet de sauvegarder ton projet sur internet, de le partager, et de collaborer avec d'autres personnes. GitHub utilise Git sous le capot.

> En résumé : **Git** = l'outil qui gère les versions. **GitHub** = le service en ligne qui stocke et partage ton code.

Ces deux outils sont au cœur du travail de tout développeur, quel que soit le langage ou le type de projet.

---

## Installation sur Mac

### 1. Installer Git

Ouvre le **Terminal** (Cmd + Espace, tape "Terminal") et lance :

```bash
git --version
```

Si Git n'est pas installé, macOS propose automatiquement d'installer les **Xcode Command Line Tools**. Clique sur **Installer** et attends la fin du téléchargement.

Vérifie ensuite l'installation :

```bash
git --version
# git version 2.x.x
```

> **Alternative via Homebrew** (recommandé pour avoir la dernière version) :
> ```bash
> /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
> brew install git
> ```

---

### 2. Configurer Git (à faire une seule fois)

```bash
git config --global user.name "Ton Nom"
git config --global user.email "ton@email.com"
```

---

### 3. Configurer une clé SSH pour GitHub

Pour que ton ordinateur puisse communiquer avec GitHub sans te demander ton mot de passe à chaque fois, il faut créer une **clé SSH**. C'est une paire de clés : une privée (qui reste sur ta machine) et une publique (que tu donnes à GitHub). Quand tu fais un `git push`, ils se reconnaissent automatiquement.

**Étape 1 — Générer la clé :**

```bash
ssh-keygen -t ed25519 -C "ton@email.com"
```

Le terminal te demande où sauvegarder la clé — appuie sur **Entrée** pour accepter l'emplacement par défaut. Il te demande ensuite une passphrase (mot de passe optionnel) — tu peux laisser vide et appuyer sur **Entrée**.

**Étape 2 — Copier la clé publique :**

```bash
pbcopy < ~/.ssh/id_ed25519.pub
```

La clé est maintenant dans ton presse-papiers.

**Étape 3 — L'ajouter à GitHub :**

1. Va sur **github.com → Settings → SSH and GPG keys**
2. Clique sur **New SSH key**
3. Donne un nom (ex: "Mon MacBook") et colle la clé dans le champ **Key**
4. Clique sur **Add SSH key**

**Étape 4 — Vérifier que ça fonctionne :**

```bash
ssh -T git@github.com
# Hi ton-pseudo! You've successfully authenticated...
```

Si tu vois ce message, tout est en ordre. Tu pourras désormais utiliser les adresses SSH (`git@github.com:...`) pour cloner et pusher sans saisir de mot de passe.

---

### 4. Installer GitHub CLI (optionnel mais pratique)

```bash
brew install gh
gh auth login
```

---
## Principes essentiels

### Comment Git voit ton code

Quand tu modifies un fichier, Git ne l'enregistre pas automatiquement — il faut lui dire explicitement ce que tu veux garder. Pour ça, il utilise **3 zones** par lesquelles ton code passe avant d'arriver sur GitHub. C'est le concept central de Git, et une fois qu'on le visualise, tout devient beaucoup plus clair :

```
Tes fichiers        Zone de staging       Dépôt local         GitHub
(ce que tu vois)    (ce que tu prépares)  (ton historique)    (en ligne)

  [modifié]  →  git add  →  [stagé]  →  git commit  →  [sauvegardé]  →  git push  →  [partagé]
```

- **Tes fichiers** : c'est ce que tu vois dans ton éditeur. Tu codes ici.
- **La zone de staging** : une salle d'attente. Tu y places les modifications que tu veux inclure dans ta prochaine sauvegarde. Ça te permet de choisir précisément quoi garder, plutôt que de tout enregistrer d'un coup.
- **Le dépôt local** : l'historique complet de ton projet, stocké sur ta machine dans un dossier caché `.git`. C'est ici qu'un commit est définitivement enregistré.
- **GitHub** : la copie de cet historique hébergée en ligne, accessible depuis n'importe où et partageable avec d'autres.

---

### Envoyer son code sur GitHub : le cycle complet

Pour qu'une modification arrive sur GitHub, elle doit passer par trois étapes dans cet ordre. Impossible de les sauter ou de les inverser.

#### Étape 1 — `git add` : sélectionner ce qu'on veut sauvegarder

```bash
git add mon-fichier.js    # un fichier précis
git add .                 # tout ce qui a changé
```

Tu places tes modifications dans la zone de staging. Imagine que tu prépares un colis : tu choisis ce que tu mets dedans avant de le sceller. Tu peux très bien avoir modifié 5 fichiers et n'en inclure que 2 dans ce commit — c'est tout l'intérêt.

> **Bonne pratique :** essaie de regrouper dans un même commit les modifications qui vont ensemble. Un commit = une idée, une fonctionnalité, un fix. Pas tout en vrac.

#### Étape 2 — `git commit` : créer une sauvegarde

```bash
git commit -m "feat: ajoute le formulaire de contact"
```

C'est l'étape où tu "scelles le colis" et lui donnes un nom. Un commit est une **photo figée de ton code** à un instant précis. Il est enregistré dans ton dépôt local avec un identifiant unique. Tu peux toujours y revenir plus tard.

À ce stade, GitHub n'est pas encore au courant — tout reste sur ta machine.

> **Un bon message de commit** décrit ce que fait la modification. `"fix bug"` ne veut rien dire dans 3 mois. `"fix: corrige le crash au login si l'email est vide"` est parfait.

#### Étape 3 — `git push` : envoyer sur GitHub

```bash
git push
```

Tu envoies tous tes commits locaux vers GitHub. C'est seulement à cette étape que ton travail devient visible en ligne — pour toi depuis une autre machine, ou pour tes collaborateurs.

---

### Créer un dépôt sur GitHub et le connecter à un projet local

Quand tu as un projet sur ta machine et que tu veux le mettre sur GitHub, il faut d'abord créer un espace d'accueil en ligne, puis faire la jonction entre les deux.

**Étape 1 — Créer le dépôt sur GitHub :**

1. Va sur **github.com** et clique sur le **+** en haut à droite → **New repository**
2. Donne un nom au dépôt (idéalement le même que ton dossier local)
3. Laisse-le en **Public** ou **Private** selon tes besoins
4. **Ne coche rien d'autre** (pas de README, pas de .gitignore) — tu vas apporter ton propre code
5. Clique sur **Create repository**

GitHub t'affiche alors une page avec des instructions. Tu veux la section **"…or push an existing repository from the command line"**. Elle te donne trois commandes à copier-coller dans ton terminal :

**Étape 2 — Dans ton terminal, depuis le dossier du projet :**

```bash
# Si ce n'est pas encore un dépôt Git, initialise-le d'abord :
git init
git add .
git commit -m "first commit"

# Les 3 commandes fournies par GitHub :
git remote add origin git@github.com:ton-pseudo/nom-du-projet.git
git branch -M main
git push -u origin main
```

- `git remote add origin ...` : indique à Git l'adresse du dépôt GitHub (son "remote")
- `git branch -M main` : renomme la branche principale en `main` (convention actuelle)
- `git push -u origin main` : envoie tout ton historique local sur GitHub pour la première fois. Le `-u` mémorise la destination, les prochains `git push` seront plus courts.

Actualise la page GitHub — ton code est en ligne.

---

### Récupérer du code depuis GitHub

#### Cloner un projet existant

Si un projet existe déjà sur GitHub et que tu veux le récupérer sur ta machine, tu le "clones". Sur GitHub, clique sur le bouton **Code → SSH** pour copier l'adresse du dépôt, qui ressemble à `git@github.com:utilisateur/projet.git`, puis dans ton terminal :

```bash
git clone git@github.com:utilisateur/projet.git
```

Git crée automatiquement un dossier avec tout le code et l'historique complet du projet. Tu n'as rien d'autre à faire.

#### Récupérer les modifications d'un collaborateur

```bash
git pull
```

Quand quelqu'un d'autre a envoyé des modifications sur GitHub depuis la dernière fois que tu as travaillé, `git pull` les télécharge et les intègre dans ton code local. C'est la première commande à lancer en début de session pour être sûr de travailler sur la version la plus récente.

---

### Les branches : travailler sans risque

Imagine que `main` est la version officielle et stable de ton projet. Les branches te permettent de travailler sur une idée, une nouvelle fonctionnalité ou une correction de bug **dans un espace isolé**, sans toucher à `main`. Si ça ne marche pas, tu supprimes la branche et `main` est intact. Si ça marche, tu la fusionnes.

#### Ce qu'il faut faire avant de créer une branche

C'est une erreur classique : créer une branche alors qu'on a des modifications en cours. Ces modifications "suivent" la nouvelle branche et se mélangent avec le nouveau travail. Pour éviter ça, **pars toujours d'un état propre** :

```bash
git status          # vérifie qu'il n'y a rien en cours (doit afficher "nothing to commit")
git pull            # récupère les derniers changements de GitHub
git switch -c ma-feature   # crée et bascule sur la nouvelle branche
```

#### Le cycle de vie d'une branche

```bash
# 1. Partir d'un main propre et à jour
git switch main
git pull
git switch -c feature/mon-truc

# 2. Travailler, committer autant de fois que nécessaire
git add .
git commit -m "feat: fonctionnalité terminée"

# 3. Envoyer la branche sur GitHub
git push -u origin feature/mon-truc

# 4. Ouvrir une Pull Request sur GitHub → faire relire → merger dans main

# 5. Nettoyage : revenir sur main et supprimer la branche devenue inutile
git switch main
git pull                         # récupère le merge
git branch -d feature/mon-truc
```

---

### Points de vigilance

**Toujours faire `git pull` avant de commencer à travailler**
Si tu ne récupères pas les dernières modifications avant de coder, tu risques de te retrouver avec des conflits au moment du push — Git ne saura pas comment fusionner deux versions divergentes. Une seconde de `git pull` en début de session évite beaucoup de maux de tête.

**Ne jamais forcer un push sur `main`**
`git push --force` réécrit l'historique distant et peut effacer le travail des autres. Sur ta propre branche personnelle c'est parfois acceptable, mais sur `main` c'est à proscrire.

**`git status` : la commande à lancer en cas de doute**
Elle répond toujours à "où j'en suis ?" — quels fichiers ont changé, ce qui est stagé, sur quelle branche tu es. Prends l'habitude de la lancer souvent.

**Les fichiers à ne jamais envoyer sur GitHub**
Certains fichiers ne doivent pas être partagés : mots de passe, clés API, dépendances volumineuses. Crée un fichier `.gitignore` à la racine du projet et liste-y ce que Git doit ignorer :

```
node_modules/
.env
.DS_Store
dist/
```





## Commandes principales

### Initialisation

| Commande | Description |
|---|---|
| `git init` | Initialise un dépôt Git dans le dossier courant |
| `git clone <url>` | Clone un dépôt distant en local |

---

### Suivre les modifications

| Commande | Description |
|---|---|
| `git status` | Affiche l'état des fichiers (modifiés, stagés, non suivis) |
| `git add <fichier>` | Ajoute un fichier à la zone de staging |
| `git add .` | Ajoute tous les fichiers modifiés au staging |
| `git diff` | Affiche les modifications non stagées |
| `git diff --staged` | Affiche les modifications stagées (prêtes à committer) |

---

### Committer

| Commande | Description |
|---|---|
| `git commit -m "message"` | Crée un commit avec un message |
| `git commit -am "message"` | Stage + commit tous les fichiers déjà suivis |
| `git log` | Affiche l'historique des commits |
| `git log --oneline` | Historique condensé (une ligne par commit) |

---

### Branches

| Commande | Description |
|---|---|
| `git branch` | Liste les branches locales |
| `git branch <nom>` | Crée une nouvelle branche |
| `git switch <nom>` | Bascule sur une branche |
| `git switch -c <nom>` | Crée et bascule sur une nouvelle branche |
| `git merge <nom>` | Fusionne une branche dans la branche courante |
| `git branch -d <nom>` | Supprime une branche (après fusion) |

---

### Travailler avec GitHub (remote)

| Commande | Description |
|---|---|
| `git remote add origin <url>` | Lie le dépôt local à un dépôt GitHub |
| `git push -u origin main` | Envoie les commits sur GitHub (première fois) |
| `git push` | Envoie les commits suivants |
| `git pull` | Récupère et fusionne les modifications distantes |
| `git fetch` | Récupère les modifications distantes sans fusionner |

---

### Annuler des modifications

| Commande | Description |
|---|---|
| `git restore <fichier>` | Annule les modifications non stagées d'un fichier |
| `git restore --staged <fichier>` | Retire un fichier du staging |
| `git revert <commit>` | Crée un commit qui annule un commit précédent |
| `git reset --soft HEAD~1` | Annule le dernier commit en gardant les modifications stagées |

---

## Workflow typique

```bash
# 1. Créer une branche pour ta fonctionnalité
git switch -c ma-feature

# 2. Faire tes modifications, puis stager et committer
git add .
git commit -m "feat: ajoute la fonctionnalité X"

# 3. Pousser la branche sur GitHub
git push -u origin ma-feature

# 4. Créer une Pull Request sur GitHub, la faire review, puis merger

# 5. Revenir sur main et mettre à jour
git switch main
git pull
```
