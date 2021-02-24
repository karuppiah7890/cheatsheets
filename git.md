# git

- Get help about git options

```bash
$ man git
# OR
$ git help git
```

- To run git commands from outside the git repository

```bash
$ git --git-dir <path-to-.git-dir> stash list
# example:
$ git --git-dir blog/.git stash list

$ git -C <path-to-git-repo> stash list
# example:
$ git -C blog stash list
```
