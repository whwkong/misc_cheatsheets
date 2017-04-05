# git workflow cheatsheet

see: <https://docs.vmfarms.com/company-policies/version-control/#process>

see: vmdocs, branch : how-to/git-specifics

Update the local repo.  

    $ whoami
    $ git ch master     # or appropriate sub-branch
    $ git pull origin master    # connects origin to the upstream

Checkout new feature branch 

    $ git ch -b <new_feature>   # new branch should be named based on the feature
    # make some changes
    $ git commit -m "message"
    $ git push origin <new_feature> 


## pushing and PRs

File a new PR in gitHub.  

## pushing to staging area 

Pushing to the staging branch for unit testing

    $ git checkout staging
    $ git pull origin staging
    $ git merge <new_feature>. 
    $ git push origin staging

Push
 
    $ git ch master
    $ git merge <new_feature>
    $ git push origin master





## reset and revert

`reset` is generally more dangerous than `revert`.  It rewinds without a history; revert leaves a historic trail.  

    git reset --soft HEAD~1     # resets the HEAD one back.  Leaves staging area and working tree intact.
    git reset --hard HEAD~2     # hard resets wipe out staging area and working tree.  


### origin

Origin is just an alias.  

    $ git push origin branchname        # sets origin to branchname



## Convenient aliases 

    git config --global alias.tree "log --graph --oneline --all --pretty=format:'%C(yellow)%h%Creset -%Cred%d%Creset %s %Cgreen%cr%Creset %Cblue%an%Creset %gn'"


 *** 


## Incorporating Changes from Master Branch into a Branch in Progress

Consider the following scenario :
- You are in the midst of making changes in a feature branch.  
- The tip of the origin/master branch has progressed from the local branch.  
- You wish to incorporate those changes into the feature branch that is still in progress.

The state can be represented as : 

```

           master             origin/master
           |                  |
    (A) −− (B)−−−−−−− (C) −− (D) 
            \
             +---(E)---(F)
                        |
                       origin/feature  

```

<br>

The recommended process for incorporating the changes from the master branch into the feature branch is :

```
$ git ch feature
  # make changes
$ git commit
$ git push 

$ git ch master
$ git pull master   
$ git ch feature-branch 
$ git merge master  # do not use git rebase 
```


### rebase vs merge

`git rebase master` does this : 

```                    

                             origin/master
                              |
    (A) −− (B)−−−−−−− (C) −− (D) -- (E) -- (F)
            \                               |
             +---(E) -- (F)                feature
                         |
                         origin/feature   

```

The problem with rebase is that the history of the branch will be rewritten, and that the parent for `feature` branch will differ from that of `origin\feature`, thus causing a diverged branch.  If there is only one contributor, and it is assured that the commit will not break the master branch, then a force push `git push origin feature -f` is acceptable.  
Otherwise if there are contributors, it's best to revert the branch to its previous state, and merge in the master branch.  
<br> 

In contrast, `git merge master` does this : 

``` 

                             origin/master
                              |
    (A) −− (B)−−−−−−− (C) −− (D) -- (G - merge commit)
            \                       /   |  
             +---(E) -- (F) -------     feature
                                        |
                                        origin/feature  

```

A separate commit (G) will be created and merged with the master branch.  In this case, the feature branch can be pushed to the upstream, and the tip of origin/master can be easily fast-forwarded.  


