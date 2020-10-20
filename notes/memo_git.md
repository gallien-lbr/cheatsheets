# Git 

|git command|action|
|-----------------------------|--------------|
|`init`|This command initialises the directory where it is executed as a Git project.Concretely, this will create a hidden ".git" directory containing all the necessary files for Git to function and to follow the modifications made inside root directory|
|`add`|Adds files to the Git index (stage or cache are synonyms for this. When a file is added in the index, it will be "tracked" by Git.|
|`commit`| Saves the index to a new commit with a message describing the applied changes (log).|
|`status`|Displays files with differences between indexes and HEADs, those with differences between the working directory and the index as well as non-tracked files|
|`branch`|List, create or delete a branch.|
|`checkout` |Allows you to move from one branch to another (and many other things)|
|`checkout -b new_branch`   | Create and move to branch|
| `checkout -- .` | Revenir sur une version précédente de la branche|
|`checkout 1eab2` | Revenir à un commit spécifique|
|`revert ID`| Revert (créer un nouveau commit qui réapplique uniquement les modifs du commit de l'ID )|
|`reset` | Revenir totalement sur une version précédente de la branche **unsafe car supprime l'historique** |
|`diff`|TODO|
|`remote -v`| Liste les différentes remotes|
|`push -u origin my_branch`|A shortcut, which doesn't depend on remembering the syntax for `git branch --set-upstream 1 is to do:`
|`push origin --delete branch_name`| delete a branch already pushed|
|`cherry-pick`| récupérer les modifs à partir d'un certain commits (sur une nouvelle branche)|


## En bref
Pour rappel, les fichiers passent par 3 "étapes" :

- espace de travail (fichiers pas encore "addés")
- Index (ou stage) (fichiers "addés" mais pas "commités")
- HEAD (fichiers "commités")

`HEAD`
Référence vers le dernier commit de la branche courante

Ajouter une remote (le nom "origin" est choisi par convention)
`git remote add origin https://github.com/{username}/{projectname}.git`

### When creating a new branch and pushing It to origin (remote)

... the first time that you push that branch. Or, to push to the current branch to a branch of the same name (handy for an alias):
```
git push -u origin HEAD
```

* https://onlywei.github.io/explain-git-with-d3/#deletebranches
* prés. méthodes retours arrières https://www.youtube.com/watch?v=RIYrfkZjWmA
* https://marklodato.github.io/visual-git-guide/index-en.html
