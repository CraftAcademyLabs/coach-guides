# Git and GitHub Workflow: Slow Food Challenge

Committing to version control:
```
git status
git add .
git commit -am 'Your commit message'
```
Push to origin - your repository on GitHub:
```
git push origin <branch name>
```

### Forking and Upstream
To make your own personal copy of a GitHub repo, you will "fork" it to your personal GitHub account. By convention, the repo you fork is called "upstream" and the repo on your personal GitHub is called "origin".

Copy the URL of the repo with the green "clone or download" button. Then in your terminal, navigate to the folder where you want to put your project folder, and use
```
git clone <URL>
```
Try `git remote -v` to see that you now have an `origin` - your personal GitHub repo.

You should have two branches - `master` and `develop`. If you fork from other repos, you may have many other branches - whatever was in the "upstream" repo. Make sure you have the `develop` branch checked out (`git checkout develop`), then:
```
git checkout -b <new branch name>
```
This will create a new branch that is an exact copy of `develop`. Make changes, commit them, then `git push origin <new branch name>`. Now your new branch will also be in your `origin` on GitHub. Once you do this, you will be able to make a Pull Request to `upstream`.

You also need to add `upstream` as a `remote`:
```
git remote add upstream <Upstream URL>
```
This will allow you to pull from `upstream` to get changes in the code. You should never `push` to `upstream`.

## Pull Requests

Once you push your new branch, head over to the Craft Academy repository on GitHub - the `upstream`. Now you will be able to make a Pull Request. That means you will be asking the coaches to merge your changes into the `upstream`. If you recently pushed your new branch for the first time, you should see your branch highlighted in orange with "compare and pull request" next to it. If you click this button, you will open the appropriate dialog. Otherwise, you'll need to go to your own repository and click "Pull Requests" and then "New Pull Request."

Look at the branches you are comparing. The one on the left should be the `upstream` - the repository on Craft Academy. The one on the right is the place where you have made changes. You should always be requesting to make changes to `develop` - not `master`. Our `master` is only for code that is tested and we are sure works.

If your code is still in progress, simply mark your PR as "WIP". When it's done, fill out the pull request dialog, then let a coach know your code is ready for review. We will be able to leave comments.

## Making adjustments to Pull Requests

If you want to change a pull request, you simply push new code to your feature branch. The pull request will automatically update.

## Merge conflicts

Often, when you make a pull request, there will be merge conflicts. This is because the `upstream` code has changed while you were working on your feature. To resolve these conflicts, you must have your feature branch checked out, then:
```
git pull upstream develop
```
The terminal will tell you where there are "merge conflicts". Open up those files, determine what code to keep and what to trash, then commit, and push again to `origin`. Your conflicts are resolved and the code is again ready to be merged.

We can't tell you exactly how to fix merge conflicts - that is a case-by-case basis. You'll need to look at the code that you used to have, the code that came from `upstream`, and the code you had in common to see what should stay. It's a good idea, in the beginning, to work as a group to make these decisions when you get your first merge conflicts.