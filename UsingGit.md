# Using Git for your daily workflow

### Installing Git

**Mac**

Install Command Line Tools using the terminal:

```
xcode-select --install```


**Linux**

Install git using the terminal:
```
$ sudo apt-get install git```

**Windows**

Have a look here to download an installing file:  [git-scm.com](http://git-scm.com/book/en/v2/Getting-Started-Installing-Git "Download file")

####Check installation
To check that the installation worked and that git is available on our computer now use

```
git --version ```

which will return information on the installed version of git.

### Configure Git
Generally you only have to make the setup once and then it keeps the changes for the future, but you can change it at any time. Use

```
git config```

to see a list of options to use.

####Choose your name and mail address
These will show up in all commits you make and thus  identify changes made by you.

```
$ git config --global user.name "Job Done"
$ git config --global user.email jobdone@example.com
```

You can use ```git config --list``` to get a list of all stored configurations.

####Choose your preferred text editor
You can set different default text editors if this is needed. You might want to use emacs, nano, or vim (How-to links for: [emacs](http://zoo.cs.yale.edu/classes/cs210/help/emacs.html), [nano](https://wiki.gentoo.org/wiki/Nano/Basics_Guide), [vim](https://www.linux.com/learn/tutorials/228600-vim-101-a-beginners-guide-to-vim)). Personally, I chose nano:

```
git config --global core.editor nano ```

### Choose a hosting service
You have different options for hosting your code online. You may consider:
**[Bitbucket](http://bitbucket.org)**
or
**[GitHub](http://github.com)**

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






More guides:

* [Beginners setup guide](http://burnedpixel.com/blog/setting-up-git-and-github-on-your-mac/)
*
