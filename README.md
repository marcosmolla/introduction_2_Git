# Introduction to Git and GitHub
## Using Git for your daily workflow
### Installing Git
**Mac**

Install Command Line Tools using the terminal:

```
xcode-select --install
```

**Linux**

Install git using the terminal:

```
$ sudo apt-get install git
```

**Windows**

Have a look here to download an installing file:  [git-scm.com](http://git-scm.com/book/en/v2/Getting-Started-Installing-Git "Download file")

#### Check installation
To check that the installation worked and that git is available on our computer now use

```
git --version
```

which will return information on the installed version of git.

### Configure Git
Generally you only have to make the setup once and then it keeps the changes for the future, but you can change it at any time. Use

```
git config
```

to see a list of options to use.

#### Choose your name and mail address
These will show up in all commits you make and thus  identify changes made by you.

```
$ git config --global user.name "Job Done"
$ git config --global user.email jobdone@example.com
```

You can use `git config --list` to get a list of all stored configurations.

#### Choose your preferred text editor
You can set different default text editors if this is needed. You might want to use emacs, nano, or vim (How-to links for: [emacs](http://zoo.cs.yale.edu/classes/cs210/help/emacs.html), [nano](https://wiki.gentoo.org/wiki/Nano/Basics_Guide), [vim](https://www.linux.com/learn/tutorials/228600-vim-101-a-beginners-guide-to-vim)). Personally, I chose nano:

```
git config --global core.editor nano
```

### Choose a hosting service
You have different options for hosting your code online. You may consider: **[Bitbucket](http://bitbucket.org)** or **[GitHub](http://github.com)**

Let us assume you registered and now have a github account.

After you created an account you might first want to create an SSH key, which will uniquely identify your computer to github so you don't have to login with your username and password every time you use git (more information on [generating SSH keys](https://help.github.com/articles/generating-ssh-keys/)). Here is a quick way to do it:

List the files in your .ssh directory, if they exist

```
$ ls -al ~/.ssh
```

Create a new ssh key, using the provided email as a label

```
$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
Generating public/private rsa key pair.
```

Save the key file

```
Enter file in which to save the key (/Users/you/.ssh/id_rsa): [Press enter]
```

Enter a passphrase. You should use a passphrase, at best long and complicated

```
Enter passphrase (empty for no passphrase): [Type a passphrase]
Enter same passphrase again: [Type passphrase again]
```

```
Your identification has been saved in /Users/you/.ssh/id_rsa.
Your public key has been saved in /Users/you/.ssh/id_rsa.pub.
The key fingerprint is:
01:0f:f4:3b:ca:85:d6:17:a1:7d:f0:68:9d:f0:a2:db your_email@example.com
```

Ensure ssh-agent is enabled:

```
# start the ssh-agent in the background
eval "$(ssh-agent -s)"
# Agent pid 59566
```

Add your generated SSH key to the ssh-agent:

```
ssh-add ~/.ssh/id_rsa
```

Add your SSH key to your account

```
# Copies the contents of the id_rsa.pub file to your clipboard
pbcopy < ~/.ssh/id_rsa.pub
```

Go to your github website and choose settings (small gear wheel in the upper right corner), click on SSH key in the list on the left. Here you can simply click on **Add Key**, give it a name and paste the key, done.

Now, let's check whether this worked. Open Terminal and enter:

```
ssh -T git@github.com
```

### Getting a Git Repository
You can get a Git project using two main approaches. The first takes an existing project or directory and imports it into Git. The second clones an existing Git repository from another server.

## Initializing a Repository in an Existing Directory

```
$ cd ~/PATH/TO/GIT/FOLDER/introduction_2_Git/
$ git init
```

This will create a ./git subdirectory that holds important files regarding your repository.

Now let's add some files to be tracked with our version control, and add a comment:

```
$ git add UsingGit.md
$ git commit -m 'adding text'
```

Before we proceed, here is how you can _clone_ an exisiting repository form GitHub (for example form the flsrgroup) to your computer.

```
$ cd ~/PATH/TO/WHERE/YOU/WANT/TO/STORE/IT
$ git clone https://github.com/flsrgroup/dplyr
```

which uses **HTTPS**, or use the following to connect via **SSH**

```
git clone git://github.com/flsrgroup/dplyr mydplyr
```

### Recording changes to the repository
Each file in your working directory can be in one of two states: tracked or untracked. Tracked files are files that were in the last snapshot; they can be unmodified, modified, or staged. Untracked files are everything else – any files in your working directory that were not in your last snapshot and are not in your staging area. When you first clone a repository, all of your files will be tracked and unmodified because you just checked them out and haven't edited anything. As you edit files, Git sees them as modified, because you've changed them since your last commit. You stage these modified files and then commit all your staged changes, and the cycle repeats.

Let's make changes to a file in our repository and see what happens

```
$ git status
```

If you add a file, it will appear as untracked, like so:

```
$ echo 'My Project' > README
$ git status
```

If you want to add this new file simply use:

```
$ git add README
```

Should you want to add a directory instead of a single file simply provide the path to `add` and it will add the files recursively. The `add` command is multi-purpose and can be envisioned as 'add to the next commit' instead of 'add to the project'. Remember, if you modify a file after you run `git add`, you have to run it again to stage the latest version of the file.

All files that are in the category 'Changes to be committed' are staged and ready to go.

```
$ git status --short
```

You want to know more about what changed in your files? Use: `git diff`to get a detailed list of all the changes.

### Committing Your Changes
We created a file (which was untracke), added it to the next commit (it is now tracked and staged), and now we will commit it using

```
$ git commit
```

The text editor will open and ask you for commit comment (as above). After entering a comment, saving and closing the editor the commit is completed.

To avoid the text editor you can also directly provide the commit message to the commit function:

```
git commit -m "Initial commit"
```

Remember that the commit records the snapshot you set up in your staging area. Anything you didn't stage is still sitting there modified; you can do another commit to add it to your history. Every time you perform a commit, you're recording a snapshot of your project that you can revert to or compare to later.

By the way, if you feel like the staging part is to cumbersome: by adding the -a option to the git commit command Git automatically stages every file that is already tracked before doing the commit, letting you skip the git add part.

And one more thing. Should you have staged a file accidentally you can unstage it with the --cached option:

```
$ git rm --cached README
```

This will remove the README file from the staging area and make the file untracked.

### Adding Remote Repositories
How to add remote repositories? To add a new remote Git repository as a shortname you can reference easily, run:

```
$git remote add [shortname] [url]

$ git remote
origin
$ git remote add pb https://github.com/paulboone/ticgit
$ git remote -v
```

More guides:
- [Beginners setup guide](http://burnedpixel.com/blog/setting-up-git-and-github-on-your-mac/)
- *
