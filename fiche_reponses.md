# Fiche de réponses : piloter GitHub depuis le terminal avec GitHub CLI

Nom et prénom : Michael Couzinet

Compte GitHub : mickcouzinet

Adresse du dépôt créé pendant le TP : https://github.com/mickcouzinet/tp-gh-cli

Système d'exploitation et terminal utilisés : Windows, PowerShell

---

## Partie 1 : vérifier l'installation et se connecter

### Q1 (section 1.2)

a) Résultat de `gh --version` et `gh auth status` :

```
gh version 2.102.0 (2026-09-30)
https://github.com/cli/cli/releases/tag/v2.102.0

github.com
  ✓ Logged in to github.com account mickcouzinet (keyring)
  - Active account: true
  - Git operations protocol: https
  - Token: gho_************************************
  - Token scopes: 'gist', 'read:org', 'repo', 'workflow'
```

b) D'après `gh auth status` :
- Protocole utilisé pour les opérations Git : https
- Autorisations (`Token scopes`) : gist, read:org, repo, workflow

Difficultés rencontrées dans la partie 1 : Aucune

---

## Partie 2 : créer un dépôt et l'explorer

### Q2 (section 2.1)

a) Résultat de `gh repo create` :

```
✓ Created repository mickcouzinet/tp-gh-cli on github.com
  https://github.com/mickcouzinet/tp-gh-cli
Cloning into 'tp-gh-cli'...
```

b) Sans GitHub CLI, les étapes auraient été :
1. Se connecter à GitHub.com dans le navigateur
2. Cliquer sur "New repository"
3. Remplir le nom "tp-gh-cli", la description, cocher "Public" et "Add a README file"/ou bien je l'ajoute à la main
4. Cliquer "Create repository"
5. Copier l'URL du repo
6. Dans le terminal : `git clone https://github.com/mickcouzinet/tp-gh-cli.git`

### Q3 (section 2.2)

a) Résultat de `git remote -v` :

```
origin  https://github.com/mickcouzinet/tp-gh-cli.git (fetch)
origin  https://github.com/mickcouzinet/tp-gh-cli.git (push)
```

- Nom du dépôt GitHub : origin
- Protocole : https
- Ce protocole a été choisi en section 1.2 lors de la connexion avec `gh auth login` (question "What is your preferred protocol for Git operations on this host?")

b) Résultat de `git log --oneline` :

```
8cb1557 (HEAD -> main, origin/main, origin/HEAD) Initial commit
```

Ce commit vient de l'option `--add-readme` dans la commande `gh repo create`. GitHub a créé automatiquement un commit contenant le fichier README.md.

Difficultés rencontrées dans la partie 2 : Aucune

---

## Partie 3 : gérer une issue

### Q4 (section 3.2)

a) Résultat de `gh issue list` :

```
Showing 1 of 1 open issue in mickcouzinet/tp-gh-cli

ID  TITLE                LABELS         UPDATED               
#1  Compléter le README  documentation  less than a minute ago
```

Colonnes :
- **ID** : Numéro de l'issue (#1)
- **TITLE** : Titre de l'issue
- **LABELS** : Labels attachés à l'issue
- **UPDATED** : Quand l'issue a été modifiée pour la dernière fois

b) `@me` désigne le compte actuellement connecté (mickcouzinet). Avantage : pas besoin de taper le nom complet, ça s'adapte directement à celui qui tape la commande.

Difficultés rencontrées dans la partie 3 : Aucune

---

## Partie 4 : ouvrir et fusionner une pull request

### Q5 (section 4.2)

a) Adresse affichée par `gh pr create` :

```
https://github.com/mickcouzinet/tp-gh-cli/pull/2
```

- Numéro de la pull request : **#2**
- Elle ne porte pas le numéro 1 car GitHub utilise la même numérotation pour les issues et les pull requests.

b) La mention `Closes #1` va fermer automatiquement l'issue #1 au moment du merge de la pull request, car c'est un mot-clé de GitHub qui lie la PR à l'issue.

### Q6 (section 4.3)

Résultat de `gh pr merge --squash --delete-branch` :

```
✓ Squashed and merged pull request mickcouzinet/tp-gh-cli#2 (docs: lister les commandes gh dans le README)
remote: Enumerating objects: 5, done.
remote: Counting objects: 100% (5/5), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 2 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), 1010 bytes | 336.00 KiB/s, done.
From https://github.com/mickcouzinet/tp-gh-cli
 * branch            main       -> FETCH_HEAD
   8cb1557..ce2f45b  main       -> origin/main
Updating 8cb1557..ce2f45b
Fast-forward
 README.md | 7 +++++++
 1 file changed, 7 insertions(+)
✓ Deleted local branch docs/1-completer-readme and switched to branch main
✓ Deleted remote branch docs/1-completer-readme
```

Actions réalisées :
1. Merge en squash de la PR #2 (GitHub)
2. Récupération de la fusion depuis le dépôt distant (dépôt local)
3. Suppression de la branche locale `docs/1-completer-readme` (dépôt local)
4. Suppression de la branche distante `docs/1-completer-readme` (GitHub)

### Q7 (section 4.4)

a) Résultat de `git log --oneline` :

```
ce2f45b (HEAD -> main, origin/main, origin/HEAD) docs: ajouter les commandes gh (#2)
8cb1557 Initial commit
```

- Nombre de commits sur `main` : 2
- Message du dernier commit : "docs: ajouter les commandes gh (#2)"
- Le numéro (#2) entre parenthèses vient du merge en squash qui intègre le numéro de la pull request au message du commit.

b) État de l'issue #1 : Closed

Résultat de `gh issue view 1` :

```
Compléter le README mickcouzinet/tp-gh-cli#1
Closed • mickcouzinet (Mcouzinet) opened about 27 minutes ago • 1 comment
```

Explication : L'issue s'est fermée automatiquement parce que la PR #2 contenait `Closes #1` dans sa description. GitHub a détecté ce mot-clé et a fermé l'issue lors du merge.

Difficultés rencontrées dans la partie 4 : Sur la commande printf que j'ai effectué sans Git bash étant sur Windows.. j'ai donc continué le TP avant de corriger ce probléme ce qui m'a un petit peu mis en difficulté pour reprendre au propre les étapes.

---

## Partie 5 : modifier le dépôt et chercher dans l'aide

### Q8 (section 5.2)

| Besoin | Commande |
| --- | --- |
| Cloner le dépôt `Hello-World` du compte `octocat` | `gh repo clone octocat/Hello-World` |
| Renommer le dépôt courant en `bac-a-sable` | `gh repo rename bac-a-sable` |
| Lister uniquement les issues fermées du dépôt courant | `gh issue list --state closed` |
| Ouvrir la pull request numéro 2 dans le navigateur | `gh pr view 2 --web` ou `gh browse 2` |

### Q9 (section 5.3)

a) Outil utilisé pour chaque action :

| Action | Outil | Justification |
| --- | --- | --- |
| Créer une branche | git | Une branche est un objet Git, elle existe dans n'importe quel repo local. |
| Créer un dépôt sur GitHub | gh | Un dépôt GitHub est un objet de la plateforme GitHub, pas un objet Git. |
| Enregistrer une modification dans l'historique | git | Un commit est un objet Git, créé et géré par Git. |
| Envoyer une branche sur le dépôt distant | git | `git push` envoie les commits et les branches au serveur distant. |
| Ouvrir une pull request | gh | Une pull request est un objet de GitHub, pas un objet Git. |
| Commenter une issue | gh | Une issue et ses commentaires sont des objets de GitHub. |

b) 
- Situation où GitHub CLI fait gagner du temps : Créer une issue, ouvrir une PR, merger une PR, lister les issues/PRs. Tout se fait en une seule commande, sans ouvrir le navigateur.
- Situation où l'interface web est préférable : Explorer visuellement un projet, lire les discussions dans les issues, voir les CI/CD status, naviguer entre les fichiers du repo.

Difficultés rencontrées dans la partie 5 : Aucune

---
