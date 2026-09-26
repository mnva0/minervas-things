This guide assumes the main SS14 project I have been working on: Triad Sector. This guide can apply about everywhere, though.
I don't use the Windows operating system, but this guide assumes Windows. For Linux users, just use Git directly.

If any part of this guide does not work, please open an issue in the GitHub page of my personal repository! I can't test all of this guide myself, so feedback would be appreciated.

# Minerva's Contributing Guide

I've decided to write this guide due to the number of people I've personally been teaching. If any of you need help, please do ask! I've taught people how to contribute *regardless* of any background.
The vast majority of contributions can't be considered to be "coding", at least in my mind. It isn't complex, nor would I even consider it programming. It's just editing files.

The asides are tangential and not strictly essential to learning. I just have a bad habit of talking too much.

These are a few useful reference links which are optional to use.
- https://ohshitgit.com/ or https://dangitgit.com/en (these are the same site) has great ways to resolve some common Git problems.
- https://docs.spacestation14.com/en/general-development/setup/git-for-the-ss14-developer.html

To start, you will need...
- A GitHub account.
- A fork of the original repository on GitHub, made under your own GitHub account. Press the "Fork" button on the top of the screen in the original repository. From your new fork, you can get the `.git` link (which Git uses) by pressing the Code button right above the file viewer on the GitHub page of your fork. This is used later in this guide and the instruction to get this link will be repeated.
- Git Bash, a command-line interface capable of using Git. This is recommended by me and the developer documentation. Command-line Git is universal and you will have a far better understanding of what you're doing.
- Some program capable of editing files. `VSCode` or `VSCodium` works fine, but whatever you might already have installed would probably work as long as it isn't Microsoft Word.
- A simple first project. If you're unsure, please ask a maintainer (ideally me) or ask in a development channel to maybe be assigned a simple one. Or find an easy idea post or bugfix. Ideas are usually easier.

Aside: why do you need these things?
- You can't make PRs or forks without a GitHub account.
- Forks let you keep your changes separate from other contributors, as well as gives you a safe place to keep your changes.
- A simple project is *strongly recommended* while you're getting used to Git. Some people may detail exactly how to implement certain things, which is ideal.

Aside: why is Git Bash recommended?
- I (as well as the docs, though maybe for other reasons?) recommend Git Bash because command-line Git is extremely simple, transparent, and easy to support because I personally use command-line Git. I can give far better support to people using Git Bash.

Open Git Bash to where you'd like to download the repository to. We'll have to configure it first. Use the following commands.
`git config set --global user.name "your github username"`
`git config set --global user.email "your github email"`
If you don't want to reveal your email, please use the email GitHub provides to you at https://github.com/settings/emails. You should additionally enable "Keep my email addresses private" if you're concerned. Using your email for a PR means it will *likely permanently be in history.*

If those commands didn't cause any messages to appear, they worked fine. You can double-check to confirm by using the following.
`git config get --global user.name`
`git config get --global user.email`

Aside: navigating folders/directories (same term) using Git Bash, in case you're not where you want to be.
- `pwd` (stands for point to working directory) tells you where you are.
- `ls` (stands for list) lists everything in your current directory.
- `cd` (stands for change directory) lets you move to another directory. Use `cd ..` to go backwards by one.

Now we're ready to download the repository. We *must* do this using Git, otherwise there might be problems. Use this command to download your fork as a local repository. To get the URL, press the "Code" button just above the file viewer in your fork's page on GitHub. It may take some time to clone.
`git clone (the .git link of your fork here)`

After that is done, `cd Triad_Sector` to get into your newly-cloned local repository. Let's try to get a devenv (developer environment) running before doing anything else. A few things have to be run first.

`./RUN_THIS.py` will download the engine: RobustToolbox. This may error—possibly due to not having Python. Download Python if it doesn't work.
`./Scripts/sh/buildAllDebug.sh` will build the game. This will undoubtedly error and ask you to download .NET, the programming language behind the game. It tells you where to go.
Building is the step that will likely take the longest. You will get around 2200~ warnings. Don't mind these.
You only have to rebuild to change configuration or when changes to C# files are made. You do not have to rebuild when making YAML changes.

Finally, you can run the server. I personally recommend the following:
`./Scripts/sh/runQuickServer.sh` will start the server, and you will be able to join it using your regular launcher by direct connecting (use the + button next to the refresh button) to `ss14://localhost` when it *does* start.

When you're done with the server, you should shut it down. Type "shutdown" in the console ingame or press CTRL+C on the Git Bash window with the server running.

*Now* we can start contributing.

We'll need a fresh branch (a parallel version of your local repository in a way) to hold your changes in. Do not continue on the "main" branch, as that should be kept clean for new branches to be made from. The maintainers will not accept PRs (pull requests) made from your "main" branch.

`git status` will show you an **overview of your changes**, including which branch you're on.
`git branch your-new-branch-name-here main` can create a new branch off of your current one.
`git checkout your-new-branch-name-here` can swap you to that branch.
Alternatively, you can use `git checkout -b your-new-branch-name-here` to create it *and* swap you to it.

Now that you have a place to keep your changes, it's just a matter of editing the files for whatever your project is. If you're unsure where to find something, use `CTRL+SHIFT+F` in VSCode/VSCodium to do a search across everything.

When you make changes to upstream (as in: not our) files, please leave a YAML comment saying that Triad has made changes there.
- If you're only changing a few lines, adding `# Triad` after each line is fine.
- If you're adding more (or if it would be cleaner), you may add `# Triad changes` on the line above and `# End Triad` on the line below your changes. This is called a block comment.
- If you're removing something, please prefix the line with `#` and add `# Triad removal` at the end.

After you make changes, you should test them by following the steps to start the server above. You should take a screenshot for the pull request later, if you'd like.

When your changes are tested and functional, you're ready to continue! First, we need to "stage" (or "add") your changes to tell Git we want to commit them to *properly* make the changes.
- Use `git status` to see your changed files and `git add changed/file/here` on each.
- `git add .` will try to add everything it can.
- `git add -p` is an alternate interactive way of doing this, allowing you to select *exactly* what you do and don't want to keep. Y to keep, N to skip. This is personally what I use.

With files added (you can use `git status` again to double-check) to tell Git we want to commit them, now we can commit them.
`git commit -m "description of your changes"` will commit *everything* you added, putting it into a form that GitHub will accept.
`git push origin your-branch-name-here` will push your commits to your fork! This may prompt you for login.

After you push your changes successfully, go to the original GitHub page (not your fork!) and you should see a new thing pop up near the top saying you can make a pull request asking to get your commits into the game!

Maintainers may make requests about things or maybe you want to add more to your PR. To do this, just do these again: stage your changes, commit your changes, push your changes. This will update your PR.

## Common problems
### remote: Permission to Triad-Sector/Triad_Sector.git denied
This occurs when trying to `git push` directly to our repository, which probably means you cloned our repository instead of your fork of our repository. If you run `git remote show origin`, it will show you a lot of information. In this instance, we care about the push URL. By default, this will point towards the `.git` URL you cloned from.

If the URL doesn't point to your fork, use the following command. This will cleanly change where the remote is pointing to.
`git remote set-url origin (the .git URL of your fork here)`

## Mapping
Mapping is a bit tricky and I am not a mapper, nor have I taught mapping. I can only confidently cover the absolute basics. I'd recommend getting someone to teach you.

- Build in the Tools configuration by using `./Scripts/sh/buildAllTools.sh`. If you use any other configuration, I believe you'll crash?
- Use the `mapping (any unused number, I use 1000)` to get into a place to map. If you need to go back and forth from the new map, use `tp 0 0 (map number)`.
- Use F3 to get your grid number. `savegrid (grid id) name.yml` will let you save your grid.
- `loadgrid name.yml` lets you load your grids.

## Cherrypicking
I would recommend going through the above before doing this, as this builds on top of everything else.

`git-cherry-pick - Apply the changes introduced by some existing commits`
Cherrypicking allows you to take commits from somewhere else and put them here. Git helpfully automates this.

Git has no clue *where* the commits we want are, though. So we have to add a new remote for this. Go to the GitHub repository of where you want to cherrypick from and get their `.git` url—the same one you'd use for cloning.
You can use `git remote show` to show all your remotes. The only one in there might be "origin", which is your fork or where you cloned your local repository from.
`git remote add nickname urlhere.git` (the nickname is for your own personal use)
`git fetch nickname` to update the remote. You may have to rerun this command if the repository was updated after you last ran it.

You only need to do this once for each repository you cherrypick from.

Find the commit hashes you want to cherrypick. For your sake, I recommend putting these in a list if you have multiple. If you want to copy pull requests over, look for the merge commits where it says they were merged. The hashes should look something like `cf57f2d`. A bunch of letters and numbers. Alternatively, you can go through the commit history of files and get commit hashes.
Some commit hashes may look longer, but they still work.

To find the merge commit line under a PR (using a random PR as an example), look for something like the below. We want the hash after "commit" there.
"DDrakov merged commit **cf57f2d** into Triad-Sector:main 4 days ago"

Make sure you're on a fresh branch. When you have your commit hashes, use `git cherry-pick commithashhere` to start a cherrypick. I think Insert works for pasting?
If everything went well, it should have cleanly moved the new commit over automatically!
If not, Git has found merge conflicts and needs your help resolving them. Use `git status` and it will tell you about unmerged files.
- If you, for whatever reason, want to stop a cherrypick, you can use `git cherry-pick --abort`.
- Go through the files and look for the merge conflict markers. They look like `<<<<<<<<<<<<<<` or `==================` or `>>>>>>>>>>>>>>>>`, but your editor may specially mark them. The markers mark where the original content is and where the cherrypicked changes are.
- Your goal is to merge everything and put it in its proper place, then remove the markers. Your editor may provide a button to do this automatically, but automated "Keep original" or "Keep new" buttons aren't smart enough to resolve all conflicts.
- After the conflicts are resolved, (again, check using `git status`), you can use `git cherry-pick --continue` to finish the cherrypick.

And you're done! You can push as if you used `git commit` because `git cherrypick` makes commits.

