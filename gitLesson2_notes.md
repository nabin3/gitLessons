## want to colaborate?
To colaborate to open source first fork repo and then clone it in your local machine. Then create a feture branch to add new feature, apply change and commit it. Then
push that commit from that feature branch to your forked repo. Now make a pull request where destination will be the repo from where you forked and it's branch will 
be main and soruce will be your feature branch and your newly pushed commit. Don't forget to provide meaningful description in your pull request.

## git reflog:
```git reflog``` records every minor details. It is life savior in case of a accidental ```git reset --hard```. Can solve this type of problems with ```get merge HEAD{ref number(just integer)}```

## solving conflict:

### merging:
If their branch which we will merge in our branch has all commit then fast-forward meage will happened. If their branch has missing some commit or our branch missing 
some commit then trying to merge will create three way merge with git's own commit msg about that three way merge. But when change happen in same line in same file in 
different branch, in time of merging branch we will have merge conflict. After solving the conflict manually or using ```git checkout --ours(to keep our barnches change)/ --theirs(to keep their branche's change) the conflicting file patth``` There will happen a first forward merge(or three way merge I am in doubt).
After check out or manually editing the conflict file add it and commit  to complete the merge.
## rebasing:
same as meging but in the checkout command, used for solving conflict --ours refer to the branch on which we will rebase the present branch and --theirs refer to the 
present branch which will be recorded on top. After using checkout command use add and ```git rebase --continue``` to complete the rebase(Where we would do commit in case of meging). If accidently did a commit in case of solving rebase conflict don't panic just use ```git reset --soft HEAD~1```
