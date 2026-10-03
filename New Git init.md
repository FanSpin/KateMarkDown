New Git init

*“list steps beginning with a new (unused)*  
 *local repository and ending with the local repo*   
*syncing with a matching git remote on*    
*a second branch named feature”* 

Steps from a new local repo to syncing with a  
 matching remote on branch feature:

 1\. Initialize a new empty local repo  
**git init**

 2\. Add your first commit on the   
default branch (main)  
**echo " project" \> [README.md](http://README.md)**

**git add** .

**git commit \-m "Initial commit"**

 3\. Create an empty remote repo (GitHub/GitLab/etc.)  
      — do NOT add a README

 4\. Link the local repo to the remote  
**git remote add origin https\://github.com/\<user\>/\<repo\>.git**

 5\. Push main and set upstream tracking  
**git push \-u origin main**

 6\. Create and switch to the second branch named "feature"  
**git checkout \-b feature**

 7\. Push the feature branch to the remote and set upstream tracking  
**git push \-u origin feature**   

After step 7, the local feature branch tracks origin/feature, and  
 both repos are in sync on that branch.

