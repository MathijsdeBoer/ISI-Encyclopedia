Git is a distributed version control system that was originally designed by Linus Torvalds (of Linux fame) back in 2005. As Linux was using another source control management, which revoked it's license for the Linux project, and because there were many developers all across the world making small changes across the project, the Linux developers needed a solution that would cover all their requirements.

>[!info]
>Git was named, just like Linux, after it's creator! Linus Torvalds stated that he is "an egotistical bastard, and \[he\] name\[s\] all \[his\] projects after \[him\]self".

The concepts behind git are actually pretty straightforward. Every user has their own copy of the git repository, including the change history. This allows for offline work without interruptions. Commonly, one location is assigned as the central repository to and from which the developers push and pull the changes. You probably have heard of providers such as [GitHub](https://github.com/) and [GitLab](https://about.gitlab.com/), which offer solutions for their users to serve their repositories.

>[!info]
>While the common method is to assign one repository as the main canon, you are able to chain online copies together. For example, the [Linux repository on GitHub](https://github.com/torvalds/linux) is actually a mirror of the actual Linux repository!

# Usage
For the following examples, we'll work with the toy project called `cool-server`. The main product of a startup serving cat pictures as a software as a service subscription model. This document is meant as a way to get you familiar with the basic terms and concepts, if you want more in-depth explanations, you can consult the excellent official [Git Book](https://git-scm.com/book/en/v2).
## Initializing or Cloning
Getting a repository started is as easy as opening your favorite [[CLI|terminal]] or git GUI and typing
```shell
git init -b main
```
This will start a new git repository in your current directory with a branch called `main`. This branch will be used, as the name suggests, the most important branch. It is worth noting that there is nothing in the git code that treats this branch any different from other branches. The only guard rails here are your own adherence to best practices.

>[!info]
>Historically, the default git branch has the name `master`, for "master copy". Though in 2020 GitHub, and a little later GitLab have followed the advice from advocacy groups to change their defaults to `main`, given the connotation with "masters" during the slavery era. This has caused (and still is) a little controversy across developers worldwide, given that the term had been used outside of this context for many years.
>
>The current default branch name in git is still `master`, when not specified, however. You can change your defaults for new repositories with
>```shell
>git config --global init.defaultBranch main
>```

If you're joining a team, or want to get someone else's code on your machine you probably don't need to initialize a new repository because one already exists. Cloning a repository as is similarly simple as initializing a new one.
```shell
git clone <url>
```
Which will clone the git repository found at `url` to a directory with the same name as the git repository in the current directory. Commonly, the URL of a git repository will end in `.git`. For example: `https://github.com/torvalds/linux.git`, `https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git` or `https://gitlab.com/linux-kernel/linux.git`
## Linking to a remote server
If you first initialized your repository with the `git init` command, there is no remote repository set up. The remote repository is a copy of your repository that you want to interact with. Most commonly, this is the online repository that you'll find on GitHub, GitLab or a private server, and where other developers will also push and pull the changes to and from.

If you used `git clone`, the remote server should have automatically been set to the server from where your URL originated from. To see if you have a remote set up, run
```shell
git remote -v
```
and it should list the remotes and their URLs that have been configured for your repository.

Adding a remote is done with
```shell
git remote add <remote-name> <url>
```
`remote-name` functions as the name for future commands we might want to run with that specific remote. This does not yet set this remote as the default remote for your future commands, such as `push` and `pull`. If you don't want to specify the remote you're trying to interact with every time, you can set it as the default with
```shell
git branch <branch> -u <remote-name>/<remote-branch>
```
Alternatively, if you've got a commit ready to push, you can also run it as
```shell
git push -u <remote-name>/<remote-branch>
```

>[!Caution]
>Note that the default remote setting can be different for each branch you might have locally, and that the remote branch name may differ from your local branch name.
## Making changes
When you've got your repository set up, you can start making changes! Simply get to work on your `cool-server` project and when you're ready to save your changes you should add the files that you want to track. If that's all changes, you can run
```shell
git add -A
```
to track all changed/added files. If it's only specific ones, you can instead run
```shell
git add ./index.html ./readme.md ./license.md
```
Which will only include the changes to the specified files. The files that you've added are called "staged" changes. Unstaged changes will not be included in the commits to your repository.

When your changes are all staged, you can commit them to your repository. In other words, you tell git that the current changes should be saved as another time point in your branch's history. Committing is done with
```shell
git commit -m "Added more cats"
```
That's it! Now you've saved the changes to your repository, and you can freely make more changes.
## Pulling and pushing
Seeing as git is a *decentralized* version control system, the changes you made and committed to your local copy are not immediately represented on your remote. That is, if you made and committed changes, your collaborators can't yet access them until you push your changes to the remote. This is very simple
```shell
git push
```
When the push is successful, another user can then
```shell
git pull
```
in their local repository to download the changes that you've made! Of course, the inverse is also true, when another user has pushed their commits to the remote, then you can pull them to your own repository.

If you want to see if there are any commits you can pull from the remote, but not actually pull them, you can run
```shell
git fetch
```
to update your remote tracking information.
## Branches
Another important feature of git is the ability to branch off different versions of the repository at arbitrary points in the history. Take the `cool-server` project. We made this project to serve cat pictures to interested (and paying) users, but someone on our development team is secretly also a fan of dogs. What they want to do is experiment with the code to see if it can be updated to also serve these pictures to users, but they don't want to hinder the main development path of our project. This is where a branch can be the solution.

Dog developer may branch off the code into it's own copy that is independent of the main development branch and change the code as desired:
```text
	dev
	 |
	 |   <-- git branch dog
	 |\
	 | \
	 |  \
	dev dog
```
Now any changes to the `dog` branch do not impact the `dev` branch and dog developer can experiment to their heart's desire without risking breaking the `dev` branch code!

Now that dog developer has successfully added the dog picture functionality, they can merge the changes with `dev`:
```text
	dev dog
	 |   |    <- git checkout dev
	 |  /     <- git merge dog
	 | /
	 |/
	 |
	 dev
```
And now `dev` also contains the new functionality that was introduced in `dog`!

>[!caution]
>The above example is just a toy example. Real world scenarios would most likely also include changes to `dev` in the meantime. If those changes also affect the same files that are changed in `dog`, you have the risk of finding yourself with a merge conflict.

>[!caution]
>As with commits, the branches will not show up on your remote server until you `git push` them.