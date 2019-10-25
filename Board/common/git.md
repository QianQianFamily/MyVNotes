# git

## Copy one remote branch to one local branch

git checkout local-branch-i-want-to-revert
git reset --hard origin/remote-branch-i-want-to-copy


## Delete a remote branch
git push --delete origin BranchNameToDelete

## Git clone/pull hang/slow
git  config http.sslverify "false"