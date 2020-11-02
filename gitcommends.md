# Main git Commands

>## See git current status
```
git status
```

>## Dedicated change on git
```
git add
```

>## Add change with messages
```
git commit -m “<message>”
```

>## See all commit
```
git log
```

>## See all commit small formate
```
git log --oneline
```

>## Go back to an old commit
```
git checkout <commit message>
```

>## Go current state
```
git checkout master
```

>## Show changes
```
git diff
```
>## Show changes on this commit
```
git show <commit messages>
```
>## Show Changes between two commit
```
git diff <commit messages><commit messages>
```
>## Show changes in the file after running(git add .)
```
git diff --staged
```
>## To delete the file permanently
```
git rm <file name>
```
>## To un track delated file
```
git reset HEAD <file>
```
>## Connect pc to github
```
SSH _ key
```

>## For first-time push data on git hub
```
git remote add origin <priject name>
git branch -M main
git push -u origin main
```

>## For Push again
```
git push origin <branch name>
```


>## Clone gitHub project on PC
```
git clone <link>
```

>## Clone gitHub project on PC change Project file name
```
git clone <link> <file name>
```
>## github online changed detected on pc
```
git fetch
```


>## github online changed Aplie on pc
```
git pull
```
>## See all Branch
```
git branch
```
>## Create a new branch
```
git branch <name>
```
>## Go any Branch
```
git checkout <branch name>
```
>## Crate and go new Branch
```
git checkout -b <branch name>
```
>## To apply this branch to the main branch
```
git marge <branch name>
```
>## Delate branch
```
git branch -D <branch name>
```
>## Temporary delate file
```
git stash
```
>## Show Temporary delated code or file
```
git stash pop
```

>## Show Temporary delated code or file
```
git stash apply
```
>## See all Stash 
```
git stash list
```
>## Go stash by id
```
git stash pop <stash id>
```
>## Remove untracked files
```
git clean -f
```