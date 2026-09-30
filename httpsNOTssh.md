# —httpsNOTssh
### This might be our biggest problem **on repeat:**  
*“assuming github ssh key test was successful,*   
*why does Linux KDE still ask for passwords?”* 

If ssh \-T git@github.com succeeds   
“Hi \_\_\_\_\_\_\! You've successfully authenticated,   
but GitHub does not provide shell access.”

but Git or other tools still prompt for passwords in KDE,   
the issue is typically that Git is using an HTTPS URL   
instead of SSH, or the SSH agent is not properly handling   
the passphrase in the KDE environment.

### 1\. Git is Using HTTPS Instead of SSH

	The most common reason Git asks for a password  
 (your GitHub username/token) despite having an SSH key  
 is that the remote repository is configured to use HTTPS.

Check: Run git remote \-v. If the URL starts with https://,   
Git will not use your SSH key.

Fix: Switch the remote URL to SSH format:  
	**git remote set-url origin git@github.com:username/repo.git**   
using the correct SSH url

### 3\. File Permissions (Skipping the “PassPhrase” stuff. Ours is empty)

If the SSH key itself is being rejected, check permissions:  
\~/.ssh directory: 700  
Private key (e.g., id\_rsa): 600  
Public key (e.g., id\_rsa.pub): 644 

Summary:   
If Git asks for a GitHub password, switch the remote URL to SSH.   
If it asks for an SSH passphrase, ensure ssh-agent is running and   
integrated with KWallet in KDE.  
