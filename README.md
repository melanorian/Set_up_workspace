# Set_up_workspace
Relevant info to set up my preferred work environment 

## VS code 
### 1. Install VS code 
Info: https://code.visualstudio.com/download

### 2. Connect to remote server
Info: https://code.visualstudio.com/docs/remote/ssh

1. Install VS code compatible SSH client to connect to your servere of choice. (Putty is not supported)
    - Ensure you have installation privilede (request via ICT) 
    - on windows machine install OpenSSH for Windows (use PowerShell script, follow steps in "install_openssh.ps1", info: https://learn.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse?tabs=powershell)
      
2. Install remote SSH extension from within VS code
   
4. ctrl + shift + p , select: Remote-SSH: Add New SSH Host
   Info: https://code.visualstudio.com/docs/remote/ssh

5. ssh to your server by typing ssh username@serverofinterest

6. open config file where instructions for the ssh connection are described
    - file pathe: drive/user/.ssh/config
    - e.g. specify forwarding, username,... (see example_config)
  
7. open a terminal in VS Code
    - Terminal/New Terminal or ctrl+ shift+ ` 

7. Promt to enter password(s)
   If your connection specified in the config file includes a host jumb you might be promted to type passwords for each server. Be prepared to type passwords >1 time.

8. Re-connect to the server
   Click the icon for " remote explorer" to see the list of severs you set up connections to. Click on the server you want to connect to and you'll be propted to type out your password(s)

9. View folders on remote server in your VS Code explorer
    - open the explorer with ctrl + shift + E
    - select the folder structure you want to view
    - a new window will open with your selection, happy bowsing 

### 3. VS code for Python-based data analysis 

Prefered set-up to have VS code interface resemble R studio. 
Set up from: https://www.r-bloggers.com/2020/07/setting-up-vs-code-for-python-development-like-rstudio/ 
File path on current machine: /home/melanie/.vscode-server/data/Machine/settings.json
