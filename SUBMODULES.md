# Guide de gestion des Submodules

Ce document explique comment gérer les submodules dans le projet ubax-project.

## Structure des Submodules

```
ubax-project/
├── ubax-platform/    → Submodule (Backend)
├── ubax-web/         → Submodule (Frontend)
└── ubax-mobile/      → Submodule (Mobile)
```

## Pour les Développeurs : Premières étapes

### Cloner le projet avec les submodules

```bash
# Méthode 1 : En une commande
git clone --recurse-submodules https://github.com/spirittechrevolution/ubax-project.git

# Méthode 2 : En deux étapes
git clone https://github.com/spirittechrevolution/ubax-project.git
cd ubax-project
git submodule update --init --recursive
```

### Travailler sur un submodule

```bash
# Accéder au submodule
cd ubax-platform

# Vérifier la branche courante
git branch

# Changer de branche
git checkout develop

# Créer une feature
git checkout -b feature/my-feature

# Faire vos changements
git add .
git commit -m "Description du changement"
git push origin feature/my-feature

# Créer une PR vers develop sur GitHub
```

## Pour les Mainteneurs : Mettre à jour le Parent

Quand un ou plusieurs submodules sont mis à jour (merges, nouvelles versions), le parent doit enregistrer ces changements.

### Mise à jour depuis GitHub

```bash
cd ubax-project

# Mettre à jour tous les submodules à partir de leurs branches distantes
git submodule update --remote

# Vérifier les changements
git status
```

Vous verrez quelque chose comme :

```
On branch master
Your branch is up to date with 'origin/master'.

Changes not staged for commit:
  (use "git add <itempath>..." to update what will index)

	modified:   ubax-platform (new commits)
	modified:   ubax-web (new commits)
	modified:   ubax-mobile (new commits)
```

### Enregistrer les changements

```bash
# Ajouter les submodules mis à jour
git add ubax-platform ubax-web ubax-mobile

# Ou ajouter seulement ceux qui ont changé
git add ubax-platform

# Vérifier avant de committer
git diff --cached

# Committer
git commit -m "Update submodules to latest versions

- ubax-platform: Latest develop branch
- ubax-web: Latest develop branch  
- ubax-mobile: Latest develop branch"

# Pousser vers GitHub
git push origin master
```

### Mettre à jour un seul submodule

```bash
cd ubax-project

# Option 1 : Depuis une branche spécifique
cd ubax-platform
git checkout develop
git pull origin develop
cd ..

# Option 2 : Via le parent
git config -f .gitmodules submodule.ubax-platform.branch develop
git submodule update --remote ubax-platform

# Enregistrer le changement
git add ubax-platform .gitmodules
git commit -m "Update ubax-platform to latest develop"
git push origin master
```

## Vérifier l'état des Submodules

```bash
cd ubax-project

# Voir le statut de chaque submodule
git submodule status

# Voir quelle branche suit chaque submodule
git config --file=.gitmodules --get-regexp path | while read _ path; do
  echo "$path:"
  git config --file=.gitmodules --get "submodule.${path}.branch"
done
```

## Workflow complet exemple

### Scénario : Développeur pousse une feature en production

1. **Développeur** travaille sur ubax-platform/develop
   ```bash
   cd ubax-platform
   git checkout develop
   git checkout -b feature/auth
   git add . && git commit -m "Add authentication"
   git push origin feature/auth
   # Crée PR vers develop → Merge
   ```

2. **Mainteneur** met à jour le parent
   ```bash
   cd ubax-project
   git submodule update --remote ubax-platform
   git add ubax-platform
   git commit -m "Update ubax-platform with new auth feature"
   git push origin master
   ```

3. **Autres développeurs** récupèrent la mise à jour
   ```bash
   cd ubax-project
   git pull origin master
   git submodule update
   cd ubax-platform
   # Maintenant ils ont la dernière version avec le feature auth
   ```

## Troubleshooting

### Submodule en état détaché (detached HEAD)

```bash
cd ubax-platform
git checkout develop  # ou la branche que vous voulez
cd ..
git add ubax-platform
git commit -m "Fix: ubax-platform back to develop branch"
git push
```

### Réinitialiser les submodules

```bash
cd ubax-project
git submodule update --init --recursive --force
```

### Voir l'historique d'un submodule

```bash
cd ubax-platform
git log --oneline -n 10  # Derniers 10 commits
```

## Notes importantes

- ⚠️ Les submodules pointent vers un **commit spécifique**, pas une branche
- ✅ Toujours faire `git submodule update` après un `git pull` du parent
- ✅ Committer les changements de submodules dans le parent
- ✅ Utiliser `git submodule update --remote` pour suivre les branches

## Questions ?

Pour plus d'informations sur les submodules Git : https://git-scm.com/book/en/v2/Git-Tools-Submodules
