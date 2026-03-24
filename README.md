# Learn to use git

This is a very brief introduction to version control with git that will go through the most basic commands. You might very quickly hit the limits of this e.g. running into conflicts. For this and anything else, I would recommend the [course on version control by Software Carpentry](https://swcarpentry.github.io/git-novice/).

## Getting started

1. Download the cheatsheet [here](https://education.github.com/git-cheat-sheet-education.pdf), bookmark it for later or print it out. No need to memorise any commands apart from the ones you need most regularly.
2. Fork and clone this repository in your home directory on the cluster.
3. Make sure you have a github account. Add your credentials on the server. 
4. Set up an ssh connection between your github account and the cluster. This will allow you to easily push changes to your code to github. See ssh_instructions.md for instructions.

## The basic idea

git can run locally and (when using platforms like Github or GitLab) sync with a remote system and act like a backup. You can think of the structure of work project as a tree with branches. Below I explain some of the most important terminology.

**Repository** -- this is what we call the folder that you use for one project

**Branch** -- if you develop your work in different directions, you might want to create a new version of your code that doesn't jeopardise your work so far. This is what branches are for. They are separate instances of your code that are neatly bundled together within a repository. You can switch between branches easily and when you are happy with work on an alternative branch, you can merge the work there back into your main branch.

**Commit** -- As you grow your tree, your project, you add commits to your repository. Think of them as mini-milestones. They are extremely useful as checkpoints. If you mess up your code, you can easily go back to your last commit.

## Make your first commit

1. Add a sentence to the `work.txt` file. 
2. Stage and commit your changes locally.
3. Push your changes to the remote repo.

Once you the work on this new branch is ready, you might want to merge it into your new branch. This is what pull requests are for. I find it easiest to do this directly on github. Pull requests can get a bit messy so I will leave you to explore them once you had a bit of practice using git. (Remember that LLMs are your friends here! Just make sure you know what you're doing when an option includes anything like `--hard`)

## Start collaborating

1. Make a new branch, switch to it and commit some changes.
2. Invite a friend to your repo and ask them to pull your new branch and make some changes too.
3. Try to pull your friends changes to the new branch. 

## `.gitignore` files

You want to avoid putting large data files in your git history, these should ideally live in a separate directory, but if you do save data within your repository, you can add a folder or a certain file ending to your `.gitignore` file. As the name suggests, git will then ignore the file and you don't need to worry about version control for it.

1. Make a csv file in your repo and add some dummy data.
2. Check the status of your repo.
3. Add `.csv` files to your `.gitignore`, now check the status of the repo again.
