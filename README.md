# Set up workspace
Relevant info to set up my preferred work environment 

## VS code 
### 1. Install VS code 
Info: https://code.visualstudio.com/download

### 2. Connect to remote server
Info: https://code.visualstudio.com/docs/remote/ssh

1. Install VS code compatible SSH client to connect to your server of choice. (Putty is not supported)
- Ensure you have installation privilege (request via ICT) 
- on windows machine install OpenSSH for Windows (use PowerShell script, follow steps in "install_openssh.ps1", info: https://learn.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse?tabs=powershell)
      
2. Install remote SSH extension from within VS code
   
4. ctrl + shift + p , select: Remote-SSH: Add New SSH Host
   Info: https://code.visualstudio.com/docs/remote/ssh

5. ssh to your server by typing ssh username@serverofinterest

6. open config file where instructions for the ssh connection are described
- file path: drive/user/.ssh/config
- e.g. specify forwarding, username,... (see example_config)
  
7. open a terminal in VS Code
 - Terminal/New Terminal or ctrl+ shift+ ` 

7. Prompt to enter password(s)
   If your connection specified in the config file includes a host jump you might be prompted to type passwords for each server. Be prepared to type passwords >1 time.

8. Re-connect to the server
   Click the icon for " remote explorer" to see the list of severs you set up connections to. Click on the server you want to connect to and you'll be prompted to type out your password(s)

9. View folders on remote server in your VS Code explorer
- open the explorer with ctrl + shift + E
- select the folder structure you want to view
- a new window will open with your selection, happy bowsing 

### 3. VS code for Python-based data analysis 

Preferred set-up to have VS code interface resemble R studio. 
Set up from: https://www.r-bloggers.com/2020/07/setting-up-vs-code-for-python-development-like-rstudio/ 
File path on current machine: /home/melanie/.vscode-server/data/Machine/settings.json

## GitHub

### Why use gitHub?
GitHub helps you to keep track of your codes' versions, facilitates sharing and publishing your code in accordance with best practices on reproducibility, collaborating with others on shared projects, last but not least, you store your code at a safe location. To get the most out of GitHub you should safe your code at regular intervals e.g. at the end of every working-day, after major changes in your code e.g. fixing a bug, and tag a version that you used to generate output files, if you continue modifying your scripts afterwards. Once you establish your workflow using gitHub, it'll be easy to maintain and trace your work.

### Set-up GitHub

#### 1. Create a gitHub account and set up 2FA authentication for logging in.
#### 2. Check/ensure that Git is installed on the machine you work on
   
Type `git --version` to see which version of git is installed, if any. If a version is returned, you are ready to go. If not, check the link below to help you set up git:

https://docs.github.com/en/get-started/getting-started-with-git/set-up-git

#### 3. Set-up an SSH key for authentication
To connect your gitHub account with your server you need to use an authentication protocol. To avoid using a password every time we will use an SSH key for authentication. For this, you generate/use a private key and a public key on your computer and deposit your public key on gitHub.

####   a) Check if you already have an SSH key
- move to your home directory
- type `ls -a`
- you'll find a hidden directory called /.ssh
- check the content of this directory `ls`
- an SSH key should look like this: id_ed25519  id_ed25519.pub - the .pub is your public key, the other file is your private key
- if you already have an SSH key, skip the following step of generating an SSH key 
   
####   b) Generate an SSH key
- find detailed instructions at: https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent#generating-a-new-ssh-key
- navigate to the /.ssh directory
- type
   `ssh-keygen -t ed25519-sk -C "your_email@example.com"`
  to generate an SSH key using the Ed25519 algorithm. Note: not all algorithms are supported by GitHub.
- You'll be prompted to answer a number of questions e.g. change the name of the key, add a pass phrase/ pass word: skip those fields by pressing ENTER
- you should now see the key in your ./.ssh directory listed at id_ed25519  and id_ed25519.pub

 ####  c) Add your public key on GitHub for a smooth authentication
- follow instructions at https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account#adding-a-new-ssh-key-to-your-account
- copy your public SSH key:
    `cat ~/.ssh/id_ed25519.pub`
- Navigate to your gitHub account in your browser
- In the upper-right corner of any page on GitHub, click your profile photo, then click  Settings (little wheel icon)
- in the "Access" section of the sidebar, click  SSH and GPG keys.
- Click New SSH key or Add SSH key.
- In the "Title" field, add a descriptive label for the new key, e.g. the name of the server you work on "PMI_server"
- Select the type of key as authentication
- In the "Key" field, paste your public key.
- lick Add SSH key
- If prompted, confirm access to your account on GitHub. For more information

Yeahhii, we successfully generated an SSH key for authentication

### Safe your code on GitHub

Note: When you use GitHub for the first time on a new server you might be prompted to sign in using your GitHub associated e-mail and password. 

#### 1. Create a new project on GitHub and clone it to your machine
When you start a new project, this is the easiest way to get started. You create a repo on GitHub (browser) and clone it to your machine.

#### a) Create a new repository on GitHub
- log into your GitHub account using your browser
- navigate to the list of your repositories (https://github.com/USERNAME?tab=repositories)
- click "New" (green button right corner)
- Fill in repo name, owner, select public/private repo, description of the repo
- "Create repository" (green button at the end of the page)

#### b) Clone the new repository to your machine
- navigate to your new repo/ the repo you want to clone in the browser version of GitHub
- click on "Code" (green button upper right side)
- select SSH and copy the link, the format should follow git@github.com:USERNAME/reponame.git
- switch to the terminal of your machine
- navigate to the location where you want to clone your GitHub repo
- type `git clone` + git@github.com:USERNAME/reponame.git
- press enter and possibly confirm your choice of cloning your repo

You should now see the repo you created on GitHub cloned on your server!

#### 2. Push an existing directory on your machine to GitHub
If you already created/worked on a project on a machine you can still push it to your GitHub and enjoy all the advantages. I assume you already set up the SSH key, now follow these steps:

#### a) Create a git repository on your machine
- navigate to your projects' directory on your machine
- Type `git init`. This will create an empty Git repository. 
- Type ` git add .`. This will add the files in the directory to the newly created git repository and prepare the content staged for the next commit.
- Type `git commit` This command commits all repo changes https://git-scm.com/docs/git-commit

#### b) Fill your remote GitHub repository with the code base on your machine
This section connects your local repo to the remote GitHub repo, renames the current branch to main and pushes the main branch to GitHub setting it as the default upstream branch for future interactions 
- navigate to your repo list in the GitHub browser
- create an empty repo with the name of the project you have on your machine
- After creating the empty repo you will find instructions to push an existing repo from the command line

```
git remote add origin git@github.com:USERNAME/reponame.git
git branch -M main
git push -u origin main
```
Happy GitHubbin

#### 3. Basic commands for using git

- `git status` check the status of your repository
- `git add` from your working directory you add changes to the staging area
- `git commit` from the staging area you commit changes to your git repository
- `git push` Creates a copy of your local git repo in the remote repo
- `git pull` updates local git repo with changes made on the remote repo, careful, if you modified both versions you'll run into a merge conflict that needs to be resolved. Git will not know which changes are the "correct" changes that you want to keep

## Transfer data

If you want to transfer data from your local machine to a remote server you can use:

`rsync -avz --progress ./your_machine_directory/your_file.extension your_target-server:"/remote_server_directory/your_target_directory"`
