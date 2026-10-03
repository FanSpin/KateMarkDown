# steps for Redirecting Branches
## Q/A from our "Brave browser (Ai chat box)"

*“list git hub steps to redirect a local repository*   
*named MadeKateWork from branch second*  
*to another branch ga-78”*

Assuming you want to switch your local repo   
from branch second to branch ga-78   
and sync it with GitHub:

Navigate to the repo  
**cd "MadeKateWork"**   

Check current branch (confirm you're on second)  
**git branch**   

Fetch the latest remote branches  
 (in the case ga-78 exists on GitHub)  
**git fetch origin**   

Switch to branch ga-78 (it does exist on remote)  
**git checkout ga-78**   

Push to GitHub (if newly created)  
**git push \-u origin ga-78**  
