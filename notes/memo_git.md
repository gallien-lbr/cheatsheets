# Git 

`init`

This command initialises the directory where it is executed as a Git project.
Concretely, this will create a hidden ".git" directory containing all the necessary files for Git to function and to follow the modifications made inside root directory.

`add`

Adds files to the Git index (stage or cache are synonyms for this).
When a file is added in the index, it will be "tracked" by Git.

`commit`

Saves the index to a new commit with a message describing the applied changes (log).


`status`

Displays files with differences between indexes and HEADs, those with differences between the working directory and the index as well as non-tracked files

`branch`

List, create or delete a branch.

`checkout`

Allows you to move from one branch to another (and many other things)

Create and move to branch
`git checkout -b new_branch`


Revenir sur une version précédente de la branche
`git checkout -- .`

Revenir sur une version précédente de la branche

`git reset`

`git diff`

Branche `HEAD`

Référence vers le dernier commit de la branche courante