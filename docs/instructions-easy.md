# Engineering Fundamentals 01 - Git - Hands On

1. Find Repository - In order to contribute to any OpenSource project you need to find where it's located. Because you are reading this, you have already found the place where this repository is located. Explore the repository somewhat by clicking around in GitHub and return here once you are ready to continue.

2. Fork Repository - Since you don't have access rights directly into this repository, you have to create a copy of this repository in order to be able to contribute. You'll have full control of your copied version of the repository so you can push changes there and eventually you'll ask the maintainer of this repository to incorporate those changes. A copy or a clone of a repository that happens on the server side is often referred to as a "Fork". On the top of any repository in GitHub, you'll find the "Fork" button. Click this button to initiate the "Fork" process and follow the instructions. After a little time, you'll be re-directed to your own version of this repository. From now on, it doesn't matter if you continue reading these instructions from the original place of from your forked repository, they are likely to be the same anyway.

3. Clone Repository - Cloning a repository will make a local copy on your computer that you can easily work on using the tools you are used to work with. Open a terminal window where you have access to the git command and execute the following command in a working folder of your choice:

```bash
git clone https://github.com/<your-git-name>/ef-01-git.git
```

> You can find the above needed URL from any repository by clicking on the Green Button named "Clone or download" on the main page of the repositories site on GitHub. 


4. Change directory - Change the current directory to the newly created one that contains your cloned repository and double check that it's indeed a Git-repository by executing `git status`:

```bash
cd ef-01-git
git status
```

5. Setup Remote to "Upstream" - There is a possibility that others will update the source repository while we are working on this local copy, therefor it's important that we can incorporate those changes if they happen. One popular way of doing that is to register a second remote (often called upstream) to make it possible to "pull" changes directly from that repository. Execute the following commands to create and view the resulting registered remotes. *Notice that the URL should be left like this for everyone, since everyone have the same "upstream" remote*:

```bash
git remote add upstream https://github.com/krist00fer/ef-01-git.git
git remote -v
```

6. Test Project - If this would be a proper development project this would have been a good time to test that everything works according to how you expect it to behave, after all you haven't changed anything right now, so if it doesn't work, it's not your fault... right?

7. Create Branch - Since we are making changes that we are not sure will be accepted right away and we don't want to disturb the main branch, we should start by creating a branch to work in. Execute the following commands to create and list what branches you have. *Notice that "greeting" can be replaced by any name you decire, but these instructions will use this name to represent this branch*:

```bash
git branch greeting
git branch
```
8. Checkout Branch - We should now have to brances `master`and `greeting`. You might have noticed a `*`next to one of the branches returned by the `git branch` command, this identifies what branch you are currently working with. You can get similar information by executing `git status`. To change into the newly created branch, execute:

```bash
git checkout greeting
```

9. Create your script file - You are now working in your own branch, in your local repository, cloned from GitHub that was previously forked from the repository you want to contribute to. Phuuu, might seem like a lot of steps but we are doing just fine. Now it's time to actually implement something. The assignment asked us to create a script in the `src/greetings` folder. One way of doing that would be to invoke Visual Studio Code from the command line by executing the following statement. Replace :

```bash
code ./src/greetings/hello-<your-name>.py
```

> If you don't want to implement the script in Python then pick another extension to better fit the language of your choice.

10. Implement the code - If you followed the above instructions you should now have Visual Studio Code open with an emtpy file. Copy past the following Python code into the file to implement the required logic. *Notice: Replace Kristofer with your name.*

```python
print("Hello Kristofer")
```

11. Test your changes (optional) - It's important to test early and often so we don't introduce problems in the code base and for the team. In this excercise this step is optional since we are not focusing on the code aspects at this time. If you do have python installed execute your script by:

```bash
python <path-to-your-file>
```

> Some Python installations will require you to write commands like `py`or `python3` to correctly execute your script. This is outside the scope of this exercise and if you run into trouble, just assume that this part is correct and continue. WARNING! Never skip tests in real life.

12. Stage your changes - Make sure you saved the changes to the newly created file above and return to the terminal window. *You don't have to close Visual Studio Code if you don't want to.* Stage your changes by executing the following. *Notice: Make sure you are in the root folder of the ef-01-git project, otherwise git might not find the changed files. Also, the command `git status` can be omitted but help you understand what's happening.* 

```bash
git status
git add .
git status
```

13. Commit your changes - If everything looks according to expected, with one file tracked, then we are getting ready to commit our changes to our local repository. Execute:

```bash
git commit -m "<Put your own short commit message here>"
git status
```

14. Integrate changes from "upstream" - Potentially someone have already updated the original repository and there might be changes there that we need to be aware of. So we need to check if that has happened or not. We do that using two commands. First we switch to the "master" branch with the `git checkout` command and then we pull down any potential changes from the `upstream` repository's master branch using the `git pull` command. If you are "lucky and first" then you'll not receive any updates and neither have any problems. Execute the following commands:

```bash
git checkout master
git pull upstream master
```

15. Merge potential changes - If there were changes that got pulled down from "upstream" we can incorporate these into our "development branch" called `greeting`. Incorporate the changes in two steps, first we change back to the `greeting` branch, then we execute the `git merge` command to take those changes and merge them with ours.

```bash
git checkout greeting
git merge master
```

> This exercise is created to avoid problems since most merges will work automatically due to the fact that most everyone will have a name that is unique (but not necessary). In real life, there will be changes that conflict with the ones you want to make and sometimes those can be quite tricky to solve. These kind of conflicts are named "Merge Conflicts".

> If merge conflicts occurrs that you are unable to solve, connect with your instructur or a colleague for help.

16. Commit the merge - If a merge happened, we need to commit it. Git automatically stage the merge for you, but doesn't automatically commit the changes. This allows you to check that everything worked out according to your beleifs (i.e. you should test again at this point). Use `git status` to see if there are uncommited files and commit them using `git commit` if necessary:

```bash
git status
# Check to see if you have uncomitted files and execute next command if so
git commit -m "<your short merge commit message>"
```

17. Push your changes to your GitHub Repository - Time to push your changes up to your repository on GitHub. The command `git push` will do that for us, but first time it'll fail since the branch that we are working on doesn't exists in your repository on GitHub. The good thing is that Git will tell us exactly what we should write to fix this. So execute `git push` and expect it to fail, read the message and then execute the suggested command.

```bash
git push

# READ THE OUTPUT
#
# fatal: The current branch greeting has no upstream branch.
# To push toe current branch and set the remote as upstream, use
#
#  git push --set-upstream origin greeting
#
# Then execute the suggested command

git push --set-upstream origin greeting

# If you need to push additional changes you can just use git push directly from this branch.
```

18. Use GitHub's User Interface to create a Pull Request - Your changes should now be visible in your repository on GitHub. *Important: Make sure you are looking at your forked repository and not the original repository since your changes won't be there yet.*. On your repositories main page, you can see a button named `Branch: master`, you can click on that one to `checkout` another branch in the user interface. *Notice that clicking and changing things in this web user interface will not automatically change things on your local repository.* Another button that has now been enabled on your GitHub Repository is the `Compare & pull request`. This  button has been highlighten since GitHub have understood that you have made changes that hasn't yet been accepted by the repository that you `forked` from. Click on that button to start the registration of your `Pull Request`or `PR`. Make sure the title of your `PR` describes what changes you have done and make sure the description even more tells what changes you are proposing and why. Once you are done click the `Create pull request` button to finally create the pull request.

19. Some human interaction required - You have now asked the maintainers of your source (upstream) repository to take a look at the changes you are suggesting. Depending on your suggestions, time constraints from the maintainers, etc. some time might pass here. The `pull request` you created in the above step was given a number so you can always get back to this `PR` later to check the status. It's not uncommon that you'll receive a comment or question in the chat system attached to the `PR`and it's up to you to monitor that. If you have done everything correctly and there are no questions asked then your PR might be accepted and merged into the repository and your mission is complete. If you are asked to do additional tasks (for example if your `PR` breaks the build) then go fix those changes locally and push them to your fork. As soon as your fork is updated, then the PR will be updated as well.

> Contributing to someone else's repository is equally much a social game as a technical challenge. Being nice, following the rules, etc. will give your PR much higher chance of being accepted than the other way around.

20. Synchronize local repository - At some point, your PR will hopefully be accepted and incorporated into the master branch of the upstream repository and your assignement is done. If you wanted to continue there are a few steps needed to clean up your local and forked repository.

```bash
# Switch to the master branch 
git checkout master

# Pull latest changes from upstream. If your PR has been accepted those changes will now include your changes.
git pull upstream master

# If your changes are now incorporated into the master branch, we don't need your local branch any more. Delete your local branch with the following command.
git branch -D greeting

# Your local repository is now in sync with your "upstream" repository, but your forked version on GitHub isn't yet up to date. We can update our forked repository (our origin remote) with the following command.
git push --force
```

> Warning - Anytime you use the flag --force you should be a bit cautious. The same goes here with `git push`. At this point, this is indeed what we want, but make sure you don't accidentaly overwite things you didn't want to.

21. Repeat from number 6 - You are now done and have successfully contributed to an OpenSource repository using a common pattern to handle change using Pull Requests. If you want to contribute more to the same project just start over from bullet 6, where you created a `feature branch` to contain your proposed changes.

Thanks for you participation!