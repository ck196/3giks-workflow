## 3giks workflow (development)

### Main flow

![workflow](3gikswf.png)

### Gitflow Workflow

- We will follow **Gitflow workflow**
- We can use an utility for Gitflow
- [Gitflow cheatsheet](http://danielkummer.github.io/git-flow-cheatsheet/)

### Example for feature branch workflow

- Brian create new branch based on develop branch

```
git checkout -b feature/brian develop
```


- Or using git-flow command

```
git flow feature start brian

```


- Brian add, commit some files

```
git status
git add <some-file>
git commit

```

- Brian finishes his feature

```
git push -u origin feature/brian

```

or

```
git flow feature publish brian
```

- Brian create a pull request from Github webpage

- Pablo receives pull request and takes a look. He can merge immediately or continue his feature. 

- Brian merge his feature in local

```
git pull origin develop
git checkout develop
git merge feature/brian
git push
git branch -d feature/brian

```

Or using git-flow

```
git pull origin develop
git flow feature finish brian
git push

```


- Brian testing everything on develop branch is OK. But it is better to create release branch to test.

```
git checkout -b release/v0.1 develop

```

or

```
git flow release start v0.1
```

- Brian finshes the release

```

git checkout master
git merge release/v0.1
git push
git checkout develop
git merge release/v0.1
git push
git branch -d release/0.1

``` 

or 

```
git flow release publish v0.1

```

- Put a tag

```
git tag -a 0.1 -m "Initial public release" master
git push --tags

```

- End user report an error. We need create a hotfix branch.

```
git checkout -b hotfix/bug01 master
# Fix the bug
git checkout master
git merge hotfix/bug01
git push

git checkout develop
git merge hotfix/bug01
git push

```

or 

```
git flow hotfix start bug01
# Fix the bug
git flow hotfix finish bug01

```


***Vietnamese version is comming***