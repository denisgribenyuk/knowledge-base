## Branch
### Work with branch
Список всех веток
```
git branch
```
Создать ветку и переключиться на нее
```
git switch -c new-branch
```
Переименовать текущую ветку
```
git branch -m new_branch_name
```
Переименовать другую ветку
```
git checkout master
git branch -m old_branch_name new_branch_name
```
Удалить ветку
```
git checkout master
git branch -d branch_name
```
### Rename Main to Master
Step 1. Create main branch locally, taking the history from master
```
git branch -m main master
```
Step 2. Push the new local main branch to the remote repo (GitHub)
```
git push -u origin master
```
Step 3. Switch the current HEAD to the main branch
```
git symbolic-ref refs/remotes/origin/HEAD refs/remotes/origin/master
```
Step 4. Change the default branch on GitHub to main
```
...
```
Step 5. Delete the master branch on the remote
```
git push origin --delete main
```
