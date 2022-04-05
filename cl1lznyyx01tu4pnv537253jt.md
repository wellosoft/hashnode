## How to Solve Squash Failed on GitLab

So I'm trying to merge one of the major features with lots of changes and merge conflicts then suddenly came out with this error:

```
Squashing Failed: Squash the commits locally, resolve any conflicts, then push the branch. Try again.
```


![Screen Shot 2022-04-05 at 16.13.16.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1649150015956/9danrs7DX.png)

It's happened to me several times. It took me some time before I gave up with it and get moved on with duplicating my merge requests (and asking for a re-approval from my workmate).

Now, not anymore. So here's how I solve it. 

Assume your current work branch is `awesome-feat`

+ Move back to the base branch, and ensure it's up to date.

```
git checkout main
git pull
```

+ Merge squash from the work branch. This shouldn't commit anything,  but your previous work will be moved to this branch.

```
git merge --squash awesome-feat
```

+ Confirm changes are in your files right now (If you have conflicts, you may need to resolve them first). Then, delete your work branch locally

```
git branch -D awesome-feat
```

+ Create a new branch, one with the same name, and checkout. 

```
git branch awesome-feat
git checkout awesome-feat
```

+ Your current work should be still the same, uncommitted, with a new branch that's clean with recent changes. Commit.

```
git add .
git commit -m "My new awesome feat"
```

+ Here's the tricky part: Force push that to your existing MR branch.<br> **Don't mistake it with the main branch or any other**.

```
git push --set-upstream origin awesome-feat --force
```

Your merge request should be clean without conflicts and ready to merge  🎉