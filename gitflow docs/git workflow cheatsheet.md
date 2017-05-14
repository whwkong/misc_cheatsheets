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


## HEAD^ vs HEAD~

Note : generally speaking, use HEAD~  

http://stackoverflow.com/questions/2221658/whats-the-difference-between-head-and-head-in-git

`ref~` is shorthand for ref~1 and means the commit's first parent. ref~2 means the commit's first parent's first parent. ref~3 means the commit's first parent's first parent's first parent. And so on.

`ref^` is shorthand for ref^1 and means the commit's first parent. But where the two differ is that ref^2 means the commit's second parent (remember, commits can have two parents when they are a merge).


    Here is an illustration...
    Both commit nodes B and C are parents of commit node A. Parent commits are ordered left-to-right.
    G   H   I   J
     \ /     \ /
      D   E   F
       \  |  / \
        \ | /   |
         \|/    |
          B     C
           \   /
            \ /
             A
             
    A =      = A^0
    B = A^   = A^1     = A~1
    C = A^2  = A^2
    D = A^^  = A^1^1   = A~2
    E = B^2  = A^^2
    F = B^3  = A^^3
    G = A^^^ = A^1^1^1 = A~3
    H = D^2  = B^^2    = A^^^2  = A~2^2
    I = F^   = B^3^    = A^^3^
    J = F^2  = B^3^2   = A^^3^2


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


## git tags

http://alblue.bandlem.com/2011/04/git-tip-of-week-tags.html 

### branches vs tags

- Summary :
    - branches are mutable references
    - tags are immutable references 

A branch is a label that points to a specific commit; however, any `branch` 
reference is automatically updated to point to a new commit.

A tag is created to point to a specific commit, and thereafter does not 
change, even if the branch moves on.


### examples

Tags are stored at `.git/refs/tags/`

    $ git tag                                   # list all tags
    $ git tag v0.2                              # create v0.2
    $ git tag -d v0.2                           # delete v0.2
    $ git show v0.2                             # show commit with tag
    $ git tag -a v1 -m "Version 1 release"      # create annotated tag

If you use an annotated tag, then the tag itself is an object (which allows
you to store meta-data within the tag).  The `.git/refs/tags/` entry for
the tag is itself a tag object that then points to a commit. 



